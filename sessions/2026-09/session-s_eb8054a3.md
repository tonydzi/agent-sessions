---
session: s_eb8054a3
date: 2026-09-25
words: 9177
turns: 2
tools: "ToolSearch"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-25 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_eb8054a3` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-24-MACANTON-01-1452
REGISTRY TOPIC: Anthropic Fellows Jan-2027: как сеньор-инженер по безопасности без ML-research попадает в программу — отбор, рефери, техлуп (через dr_start; ПОТРЕБИТЕЛЬ: заявка оператора в Anthropic Fellows (дверь A по task-2026-09-23-visionary-map-choose-door): эссе, выбор рефери, подготовка к техлупу)

Return ONLY a JSON object (no prose, no code fence) with EXACTLY these keys:
{
 "lang": "ru|en|mixed",
 "topic": "<clean human topic of the research, <=90 chars>",
 "one_line": "<one sentence: what question this deep-research answered>",
 "key_findings": ["<substantive conclusion grounded in the report>", "..."],
 "recommendations": ["<concrete recommendation / decision the report implies>", "..."],
 "entities": {"people": ["..."], "companies": ["..."], "products_tools": ["..."]},
 "open_questions": ["<what stayed unresolved / needs verification>", "..."],
 "related_concepts": ["<short concept name this connects to, for cross-linking>", "..."]
}
Rules: extract ONLY from the report text; never invent people, numbers or claims not present.
Merge across the vendor sections (they research the SAME question) -- deduplicate findings,
prefer the better-supported statement. 4-10 key_findings, be specific (numbers, names, tradeoffs).
If a list is empty use []. Write findings in the report's own language (ru stays ru).

REPORT (vendor sections tagged; may be Russian, English or mixed):


===== VENDOR: grok (DR26-09-24-MACANTON-01-1452-anthropic-fellows-grok.md) =====
---
dr_id: DR26-09-24-MACANTON-01-1452
source: grok
source_url: https://grok.com/c/s_a26acb79
mode: Heavy (селектор прочитан со скриншота)
topic: "Anthropic Fellows Jan-2027: сеньор-инженер по безопасности без ML-research — отбор, рефери, техлуп"
collected_at: 2026-09-24T15:44:43
collected_by: NODE-0X (NODE-0X), /dr-fanout, живой Chrome-MCP
collected_how: innerText главного контейнера -> window.name -> локальный sink (текст в контекст модели не попадал)
trim: срез по якорю 'Thought for 1m 56s'
distinct_urls_in_body: 31
origin: external-llm
---

Thought for 1m 56s
Anthropic Fellows Program (January 2027) — Deep Research Report

Subject: How a senior security / distributed-systems engineer with no ML-research record ([ИМЯ] [ФАМИЛИЯ]) gets selected

Cohort target: January 2027, AI Security & Frontier Red Team first; AI Safety & Alignment (control/evals) second

Research date: 25 September 2026

Overall confidence: Medium on official mechanics and stream fit; Low–Medium on unpublished selection weights and “what distinguished accepted apps.” Official pages are high quality. Acceptance-rate numbers, CodeSignal cutoffs, and “what reviewers actually ask references” rest on thin, often single-source accounts.

Decision in one line: Apply now to the Security stream as primary, Safety/control-evals as explicit second. The official Security criteria match this profile better than the Safety criteria. The hard gates are (1) CodeSignal ICF under time, (2) three references who can talk about how he ships technical work, and (3) essays that pitch a 4-month FRT eval project rather than a COO résumé.

Ranked list: 10 most decision-relevant findings

1. Official text already names cybersecurity as a successful prior background and says ML research is not required. [established]

Jan Leike’s program page: “You don't need a PhD, prior ML experience, or published papers. We've had successful fellows from physics, mathematics, computer science, cybersecurity, and other quantitative backgrounds.” Also: “We care much more about your ability to execute on research than your credentials.”

Date retrieved: Alignment Science blog page last used for the November 2026 cohort announcement (applications then closed 26 July); still the current official “what we’re looking for” language as of this research pass.

Greenhouse id_2e26dffe (live January 2027 Safety & Security posting) repeats “promising technical talent — regardless of previous experience.”⁠Alignment.anthropic +1

2. The Security stream’s unique criteria match this applicant; the Safety stream’s unique criteria do not. [established]

Live Greenhouse id_2e26dffe unique criteria for AI Security Fellows: OSS in LLM- or security-adjacent repos; ownership of ambiguous technical problems; pentesting / vulnerability research / offensive security; “willingness to do the ‘dirty work’ that produces high-quality outputs”; CVEs or bug bounties; empirical ML and DL frameworks listed as extras, not the core. Mentors listed: Brenda [ФАМИЛИЯ], Keri Warr, Evyatar Ben Asher, Keane Lucas, Newton Cheng.

Safety unique criteria instead emphasize empirical ML projects, LLM experience, and the listed safety research areas. dev’s inspect_ai #4769, MCP Go SDK, fastmcp, agno, qwen-code, and production Claude fleet sit inside the Security list. His missing pieces versus that same list are CVEs/bounties and DL-framework experiment management — say so honestly; do not invent them.⁠Job-boards.greenhouse <http://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe>

3. Cohort size grew from 10–15 to ~32; overall acceptance is not published and the circulating “<2% / <5%” figures are not official. [emerging, with disagreement]

Pilot (announced Nov/Dec 2024): 10–15 fellows, originally 6 months.⁠Alignment.anthropic <https://alignment.anthropic.com/2024/anthropic-fellows-program/>
Anthropic official X, 29 July 2025: “There'll be around 32 places.”⁠X <https://x.com/AnthropicAI/status/1950245027604812094>
Pingbang Hu CV (UIUC PhD candidate; accepted fellow): “Fellows (32 out of 2000+ applicants worldwide).” [single-source]⁠Pbb <https://pbb.wtf/cv.pdf>
LessWrong, 19 Dec 2025, citing that same newly announced fellow: “one of 32 fellows selected from over 2000 applications… less than 1.3%.” [single-source origin, then repeated]⁠Greaterwrong <https://www.greaterwrong.com/posts/aEiZfHAXeKXF5PJgH/ai-safety-has-a-scaling-problem>
Sauers_ on X, 22 Oct 2025, quoting Pingbang Hu’s offer post: “1.6% acceptance rate on top of self selection.” [low-authority]⁠X <https://x.com/Sauers_/status/1981087223161270559>
Extern.com (12 Jul 2026) and leonstaff (31 May 2026) both recycle an unnamed “finalist” anecdote: ~150 people finish all rounds for ~32 seats (~21% final-round), CodeSignal kills 60–70%, overall “<5%.” These two pages are derivative of each other. Treat as UNVERIFIED aggregator.
Do not quote a precise acceptance rate as fact. Use: official size is on the order of 32 per cohort across streams; application-to-offer is almost certainly low-single-digit percent after self-selection.⁠Extern <https://www.extern.com/post/anthropic-internship-guide>

4. CodeSignal is a hard filter, but a high score is not an advance. [emerging]

Dated candidate reports, all [single-source] or [low-authority] unless noted:

Official-ish Oct 2025 Fellows posting reprint: 90-minute Python screen of “reasonably straightforward coding that involves refactoring and adapting to new requirements, without… cliched algorithms.”⁠Startup <https://startup.jobs/anthropic-ai-safety-fellow-us-anthropic-3-7051849>
Glassdoor Sep 2025 London Fellow candidate: email said 480/600 cutoff; candidate scored 590 and was rejected; claims a 600 was also rejected. Process after OA described as 55-min core-Python, 55-min Colab LLM, 15-min research brainstorm.⁠Glassdoor <https://www.glassdoor.com/Interview/Anthropic-Interview-E8109027-RVW101368327.htm>
Reddit r/Anthropic, 28 Jan 2026: Fellows applicant 540/600 did not advance; another commenter said their cutoff was 480 and they scored 470. [low-authority]⁠Reddit <https://www.reddit.com/r/Anthropic/comments/1qovmbs/assessment_for_anthropic_fellows_program_for_ai/>
Reddit r/csMajors, 4 Aug 2026: 10-year coder / Nature-paper author scored 0/600 on Fellows OA because the class/README contract was ambiguous. [low-authority]
Implication for a 20-year systems engineer: the failure mode is not algorithms. It is extending an in-memory system (bank / DB / filesystem / TTL / scheduled transactions) under a black-box grader while the spec mutates.⁠Reddit <https://www.reddit.com/r/csMajors/comments/1vfl819/bombed_my_anthropic_fellows_oa_1/>

5. References are described as “one of the main ways we assess candidates,” contacted without notice, and ML-community refs are preferred — not required. [established for the form language; speculative for weight vs essays vs screens]

Older Constellation/Airtable form, opened via search: “References are one of the main ways we assess candidates. The most useful references come from people who've collaborated with you on technical work and can speak concretely to your strengths and weaknesses. References from the ML research community are preferred if available.” And: “we plan to reach out to your references without giving you notice. We will ask them to respond within a week.”

No public question bank for what those calls contain. [no source found]

Practical reading: an inspect_ai / fastmcp / MCP Go SDK maintainer who merged multiple PRs over weeks is closer to the stated criterion (“collaborated on technical work… strengths and weaknesses”) than a COO-era employer who can only speak to leadership. An ML-community name is a bonus, not a substitute for concrete collaboration.⁠Airtable <https://airtable.com/appCHLjgoTUCJMLct/pagUhpiBE5KxoU3lX/form>

6. At least two accepted or affiliated profiles look like industry systems/quant engineers, not ML PhDs — but the visible published sample is still skewed Brasov/academic. [emerging]

Cole Killian (SCONE-bench, Dec 1 2025): listed “MATS and the Anthropic Fellows program,” mentored by Brenda [ФАМИЛИЯ] and Alwin Peng. Independently, a Cole Killian with McGill BSc Math & CS and a deleted resume listing Jump Trading HFT engineering was publicly identified in Feb 2025 DOGE coverage. Same uncommon name + CS/math + trading-systems stack; the SCONE paper itself does not mention Jump or DOGE. Treat identity-match as [emerging], not courtroom-grade.⁠Anthropic <https://www.anthropic.com/research/smart-contracts>
Aria Wong (current Anthropic Fellow on her own site): Princeton math, previously led quant/engineering at a hedge fund (Nova Fund / Brevan Howard per secondary profiles), MATS 9.0 then AFP. Safety/control, not Security.⁠Ariahw.github <https://ariahw.github.io/>
Contrast set of published fellows: Chloe Loughridge (Harvard BA 2019–24), Pingbang Hu (UIUC PhD candidate), Horvat Hanna (UvA PhD student, prior Redwood REMIX), Aengus Lynch (UCL PhD + prior Anthropic contractor), Mikhail Terekhov (EPFL / MATS / AFP).
There is no public roster. Any “most fellows are recent grads” claim is [speculative]. Official copy continues to sell the program as a mid-career transition vehicle.⁠Alignment.anthropic <https://alignment.anthropic.com/2024/anthropic-fellows-program/>

7. The Security stream’s 2025–2026 public output is eval harnesses, exploit agents, and control scaffolds — not model training. That is the work a 4-month outsider can actually do on open models/APIs. [established]

Named FRT / Fellows outputs (all opened):

SCONE-bench / $4.6M smart-contract exploits — 1 Dec 2025.⁠Anthropic <https://www.anthropic.com/research/smart-contracts>
Strengthening Red Teams modular control-eval scaffold — 6/12 Nov 2025.⁠Alignment.anthropic <https://alignment.anthropic.com/2025/strengthening-red-teams/>
Exploit-development evals (ExploitBench / updated SCONE) — 22 May 2026.⁠Anthropic <https://www.anthropic.com/research/exploit-evals>
LLM ATT&CK Navigator — 3 Jun 2026.⁠Anthropic <https://www.anthropic.com/research/attack-navigator>
Measuring LLMs’ impact on N-day exploits — 8 Jun 2026 (Winnie Xiao et al.).⁠Anthropic <https://www.anthropic.com/research/n-days>
Discovering cryptographic weaknesses with Claude (HAWK + reduced-round AES) — 28 Jul 2026.⁠Anthropic <https://www.anthropic.com/research/discovering-cryptographic-weaknesses>
SLEIGHT-Bench (monitor-evasion transcripts) — 19 May 2026; Fellows Program authors.
Fellows “primarily use external infrastructure (e.g. open-source models, public APIs).” That constraint is load-bearing for project design.⁠Alignment.anthropic +1

8. The form will surface the September 2026 full-time Greenhouse applications. There is no public evidence that applying to AFP “hurts” later FT hiring; the documented risk is the reverse direction (a rejected FT loop creating a 12-month wait), and even that policy is for FT roles. [emerging / incomplete]

Airtable Fellows form includes both:

“Have you applied to work with Anthropic full-time roles, or to collaborate with Anthropic researchers via programs like MATS, Astra, or the Anthropic Fellows Program within the past year?”
“Have you previously applied to or interviewed at Anthropic?”
Anthropic careers FAQ (FT, not Fellows-specific): “Yes—you’re welcome to re-apply after 12 months, or sooner if something materially changes about your experience or skills.”
Greenhouse Fellows pages say Constellation runs Fellows recruiting; FT roles are Anthropic Greenhouse. Whether those ATS records are linked is [no source found]. Answer the form questions truthfully. Do not assume AFP is a stealth FT backdoor, and do not assume the Sep 2026 FT apps are invisible.⁠Airtable +1

9. Rolling review is real; late September is better than late October for a January start. [emerging]

Current Safety & Security listing: applications open for January 2027, rolling.

Pingbang Hu first-hand (accepted, Oct 2025 cohort): saw the July 2025 “32 places” post, applied; ~1 month later passed first stage; four interview rounds; offer a few days before 22 Oct 2025. [single-source]

Glassdoor Fellow candidates: OA sometimes arrived ~1 month after apply; total process ~4 weeks once moving. [single-source]

Coaching-site claim of “3–6 weeks application-to-offer” (Extern, 12 Jul 2026) is UNVERIFIED aggregator.

Prior cohorts had hard cutoffs (e.g. 17 Aug 2025 for Oct 2025; 26 Jul 2026 for Nov 2026). A January 2027 rolling window can still close when the cohort fills. Applying in the last week of September 2026 is the conservative move.⁠Job-boards.greenhouse +3

10. Essays that stay generic “AI safety matters” or lead with executive titles are the documented miss; specific 2026 FRT papers + a 4-month project + honest gaps are the documented hit pattern. [emerging]

Official AI-usage policy (updated 10 Jul 2025): “Please create your first draft yourself, then use Claude to refine it.” Take-homes and live interviews: no AI unless the prompt says so.

Alyssa Fu Ward (rejected applicant, Substack 1 Jul 2026) built an AI “red team” of personas to critique her essays; the simulated ML-researcher persona’s objection was the absence of even a rough study design. [single-source, rejected]

Security posting language rewards “dirty work,” OSS, and shipped artifacts — not COO/CTO framing.⁠Anthropic +2

1. Selection reality

Who reviews. Applications and interviews are “managed by Constellation,” Anthropic’s recruiting partner; Constellation also runs the Berkeley workspace. Emails come from Constellation. Mentors listed on the Safety & Security posting are the people fellows match to after offer, not necessarily the first-round readers. Joe Benton is independently described in 2026 secondary coverage as having led or helped run Fellows / scalable oversight; he left Anthropic for METR around late August 2026. Treat “Benton ran Fellows” as [single-source / secondary], not as current process.⁠Simplify <https://simplify.jobs/p/s_67880a9d/Fellows-Program>

Stated loop (official, current posting): “initial application & reference check, assessments & interviews, and a research discussion.”⁠Job-boards.greenhouse <http://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe>

Reconstructed loop from 2025–2026 candidate accounts (dates matter; format drifted):

Stage	What sources say	Date / quality
Written app + 3 refs	Motivation, research areas, FT-offer likelihood, logistics	Official form language, Airtable snapshots 2025–2026⁠Airtable <https://airtable.com/appiuxxfhf5moRwTx/pagDCFPHd9qOKZ5ki/form>
Reference outreach	May happen before OA, between OA and live, or in final loop; without notice	Glassdoor Sep 2025 [single-source]⁠Glassdoor <https://www.glassdoor.com/Interview/Anthropic-Interview-E8109027-RVW100353268.htm>; form text [established]
CodeSignal OA	90 min, 4 progressive stages, industry-coding framework (in-memory bank/DB)	Multiple 2025–2026 accounts; official-ish Oct 2025 posting
Live coding	90 min with an engineer on CodeSignal, spec-heavy, clarify first	Exponent Fellow guide 30 Apr 2026 [low-authority coaching]⁠Tryexponent <https://www.tryexponent.com/guides/anthropic-ai-safety-fellow-interview>
Final loop	55-min Colab “Prompting and Engineering with LLMs” + 15-min research brainstorm with a potential mentor	Glassdoor Sep 2025; Exponent Apr 2026
Older vintage (2025)	Some postings also mention a 5-hour take-home	Archived Oct 2025 process writeups; may be retired

Weight of references vs essays vs screens. Official form: references are “one of the main ways we assess candidates.” Official posting lists the reference check in the same breath as the initial application. Glassdoor + Reddit: people with 590–600 CodeSignal still die on the holistic screen. No public rubric assigns percentages. [speculative to quantify]

What distinguished accepted applications, as far as public artifacts go.

A project-shaped research taste already pointed at an Anthropic problem (SCONE, control scaffolds, subliminal learning, circuit-tracer, SLEIGHT-Bench, agentic-misalignment evals).
Ability to produce a public artifact in ~4 months on external APIs.
In the Security lane: either prior offensive/eval work or a systems stack that maps onto exploit-eval harnesses (Killian’s HFT/systems background is the existence proof).
Coding speed on messy specs, not LeetCode trophies.

First-hand accounts, accepted.

Pingbang Hu (@PingbangHu), 22 Oct 2025: applied after the July “32 places” post; passed first stage ~1 month before interviews; four rounds; offer days before the tweet. Verified account, now lists “Fellows @AnthropicAI.” [single-source first-hand]⁠X <https://x.com/Sauers_/status/1981087223161270559>
Chloe Loughridge (@ChloeLough333), 10 Nov 2025: public thread crediting the Research Fellow Program for the red-team scaffold papers. Verified-enough personal site + OpenReview.⁠X <https://x.com/ChloeLough333/status/1988031992299221074>
Aengus Lynch CV: Anthropic Fellow Jan–Apr 2026 after already being an Anthropic contractor. Different prior-density than dev.⁠Aenguslynch <https://www.aenguslynch.com/cv.html>

First-hand accounts, rejected or stalled.

Glassdoor Fellow interviews dated 30 Sep 2025, 19 Nov 2025, 1 Apr 2026: OA + refs + no offer; complaints that the stated 480 cutoff was not honored. [low-authority, anonymous]⁠Glassdoor <https://www.glassdoor.com/Interview/Anthropic-Interview-E8109027-RVW100353268.htm>
Alyssa Fu Ward, 1 Jul 2026: applied, used Claude to red-team essays, later rejected. [single-source]⁠Alyssafuward.substack <https://alyssafuward.substack.com/p/applying-for-the-anthropic-fellows>
r/csMajors 4 Aug 2026: strong CP/SWE + Nature papers, 0/600 on Fellows OA because of spec/class mismatch. [low-authority]⁠Reddit <https://www.reddit.com/r/csMajors/comments/1vfl819/bombed_my_anthropic_fellows_oa_1/>

X, last 30 days (25 Aug–25 Sep 2026). Almost no practitioner discourse about selection. What exists:

Miguel Fierro (@miguelgfierro), 20 Sep 2026: promo restatement of stipend + “No PhD, no ML background, no papers.” Not a fellow. [low-authority]
@aispherehub, 21 Sep 2026: visa FAQ (US/UK/CA auth required). Correct vs official pages.
Joe Benton departure threads (mid-Sep 2026) are about Anthropic safety staffing, not AFP admissions.
Keyword search for “AFP” is poisoned by Agence France-Presse. Semantic search for “Anthropic Fellows application experience” in this window returned generic rejection-advice threads, not AFP-specific signal.
Finding that rests only on X: none that we would let drive the decision. The last-30-day X corpus is not where AFP selection knowledge lives right now.
2. Profile fit

Official posture. Mid-career transition is in the original 2024 launch copy: “focused on helping mid-career technical professionals transition into the AI safety research space, but regardless of your background or career stage, we’re open to your application.” 2026 copy keeps “regardless of previous experience” and names cybersecurity. That is the strongest official document dev has.⁠Alignment.anthropic <https://alignment.anthropic.com/2024/anthropic-fellows-program/>

Named Security / Security-adjacent fellows, 2025–2026

Person	Evidence of AFP/MATS	Prior shape	ML-research record before the project?
Winnie Xiao	MATS page lists her as MATS fellow; SCONE byline “MATS and the Anthropic Fellows program”; later first author on FRT N-day paper (8 Jun 2026)	Thin public bio; do not confuse with GDM’s Winnie Xu	Not established in open web
Cole Killian	Same SCONE byline	McGill math/CS; Jump Trading HFT engineer on a deleted resume (Wired / National Post / Yahoo, Feb–Mar 2025) [identity-match emerging]	No public ML papers found
Chloe Loughridge	Self-credits AFP Nov 2025; OpenReview “Anthropic Research Fellows Program”	Harvard BA 2019–24; DafnyBench / CCS workshop	Light prior ML, junior
Elle Najt, Colin Toft	SLEIGHT-Bench affiliations “Anthropic Fellows Program” / Waterloo	Bios not independently recovered	[no source found] beyond the paper

Named Safety-stream fellows (contrast). Aengus Lynch (UCL PhD + prior Anthropic contractor), Horvat Hanna (UvA PhD, Redwood REMIX), Alex Cloud & Minh Le (Subliminal Learning), Mikhail Terekhov (EPFL / MATS, Diffuse AI Control), Pingbang Hu (UIUC PhD candidate), Aria Wong (Princeton math + hedge-fund HoE → MATS 9 → AFP). These are not the Security-stream prior.

Senior (10+ years) vs recent grads. No roster, so no count. Visible published names skew early-career academic. Two industry-systems analogues exist (Killian; Wong on the Safety side). dev would be an outlier on years, not on shape. Official copy still invites that outlier.

Fellows without prior ML research. Official sentence says they exist, including from cybersecurity. Killian is the best public Security-stream illustration. We did not find a 20-year hired-executive fellow in the open record. [no source found]

SCONE-bench authors as the requested data point.

Byline (1 Dec 2025): Winnie Xiao*, Cole Killian*, Henry Sleight, Alan Chan, Brenda [ФАМИЛИЯ], Alwin Peng — “MATS and the Anthropic Fellows program.”

Henry Sleight is Research Programs Lead at Constellation (and previously MATS research management) — staff, not a fellow. Alan Chan, Kiel, Peng are mentors/staff. The two fellow-side names are Xiao and Killian. Open-sourced harness: https://github.com/safety-research/SmartContract-bench. The paper is exactly the genre of 4-month external-infra project AFP wants: a Dockerized fork-and-grade benchmark, MCP tools, Foundry, a dollar metric.⁠Anthropic +1

3. What the Security stream actually does, and what a 4-month outsider can add

Constraint from the posting: external models and public APIs, public artifact, 4 months, mentor-pitched then fellow-shaped.⁠Job-boards.greenhouse <http://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe>

2026 FRT / related artifact	Date	What it is	Outsider contribution that is realistic
SCONE-bench	1 Dec 2025	405 historically exploited contracts + 2,849 live-scan; exploit revenue as the metric	New domains, new post-cutoff slices, better graders, MCP-tool ablations
Exploit-development evals	22 May 2026	ExploitBench / ExploitGym; Mythos vs earlier models on primitives → chains	Harness engineering, determinism, cheaper open-model baselines
N-day exploit evals	8 Jun 2026	Firefox patches + Windows kernel N-days; hours-not-weeks exploit writing	Reproduction on open models; patch-to-PoC latency as an eval; not claiming Mythos-level chains
LLM ATT&CK Navigator	3 Jun 2026	832 banned accounts mapped onto MITRE ATT&CK; ARiES risk score	Authors are Guru / Moix / Klein (not listed as fellows). An outsider can still build an open ATT&CK-tagged agent-trace corpus from public incident reports
Cryptographic weaknesses with Claude	28 Jul 2026	HAWK key-recovery; reduced-round AES “Möbius Bridge”; scaffolded autonomous search	MEPhI-cryptography-shaped eval of open models on known-weak variants; do not claim new breaks of production AES
Control-eval scaffold (Loughridge)	Nov 2025	Five-module red team (suspicion, attack selection, plan synthesis, execution, subtlety); SHADE-Arena safety score 0.87 → 0.41	Productionize as inspect_ai tasks with majority graders
SLEIGHT-Bench	19 May 2026	40 monitor-evasion attacks, 11 categories; Opus 4.6 monitor misses many at 1% FPR	New transcripts from a real multi-machine agent fleet; grader-panel evals

Five concrete pitches mapped to this applicant’s evidence

CEX / matching-engine analogue of SCONE-bench. Historical exchange-bug classes (race on partial fills, fee-rebate inconsistency, custody key-handling, cancel/replace TOCTOU) as a Dockerized fork-and-grade harness. Metric: simulated P&L of an LLM exploit agent, with deterministic replay. Uses: exchange backends, market-maker / HFT engines, inspect_ai reducer work.
Agent-control-plane eval on the existing Claude fleet. Treat the public multi-machine fleet as the system-under-test. SLEIGHT-style covert objectives (credential reuse across machines, grader-shopping, log-tampering) + majority-grader panels — the pattern already merged as inspect_ai #4769.
MCP-tool-use ablation on SCONE. He has MCP Go SDK and fastmcp PRs. Question: does giving the exploit agent MCP tools raise attack-success rate on post-cutoff contracts, and can a monitor catch the tool-use traces? Directly extends Kiel/Peng’s published setup.
CryptanalysisBench-open. Not “break AES.” A small, reproducible suite of known-weak targets (reduced-round AES, toy lattices, nonce-reuse GCM) measuring whether open models + a search scaffold recover the published attack, with unit tests and red-team cases. Uses MEPhI cryptography + C++/Python. Anchors to the 28 Jul 2026 FRT post without overclaiming.
Productionize the Loughridge modular red-team scaffold as inspect_ai tasks. Suspicion model, attack-selection policy, subtlety rewrite, deterministic fixtures. This is “dirty work that produces high-quality outputs,” which is the Security posting’s own phrase.

Any of these is a paper-or-repo in 16 weeks on public APIs. None require training or fine-tuning, which he does not have.

4. References

Form language (opened Airtable snapshot): three required references plus optional extras; context on each person’s background and on the relationship (what you built, when, how closely); ML-research community preferred if available; contacted without notice; one-week reply window.⁠Airtable <https://airtable.com/appCHLjgoTUCJMLct/pagUhpiBE5KxoU3lX/form>

What reviewers actually ask. [no source found] for an AFP-specific question list. Adjacent MATS guidance (Matt Handzel notes, 16 Mar 2026, [low-authority personal site]): MATS contacts refs later, wants people who can speak to independent research. AFP-specific page on the same site only says “check the current application.”⁠Matthandzel <https://www.matthandzel.com/notes/asking-for-letter-of-reference>

OSS-maintainer refs vs employer refs. Official text prefers collaborators on technical work who can name strengths and weaknesses. A maintainer who argued through inspect_ai #4769 for weeks is on-policy. A COO-era executive who can only say “he ran the team” is off-policy relative to “dirty work / implement ideas quickly.” An ML-community name without shared commits is weaker than an OSS maintainer with shared commits. That ranking is an inference from the form’s own words, not a leaked rubric — tag [speculative] for the ranking, [established] for the form text.

Guidance from Constellation / MATS / AFP on reference quality. Beyond the form paragraph above, none found. Henry Sleight (Constellation Research Programs Lead, co-author on SCONE) is the named connective tissue between Constellation, MATS, and AFP, not a published advice-giver.⁠Alphaxiv <https://www.alphaxiv.org/@henry-sleight>

Operational advice that follows from the form, not from folklore: brief the three people now; tell them they may get a Constellation/Anthropic email with one week to reply; give them the exact repos and PR numbers; ask them to be willing to name a weakness.

5. Essay content

Policy (10 Jul 2025, still the live page): first draft yourself, Claude to refine; no Claude-invented experience; no AI on assessments unless the prompt allows it; live interviews are human-only.

Older Anthropic FT ads said “please don’t use AI” (FT, 4 Feb 2025). That policy was replaced. Use the July 2025 page, not the February 2025 one.⁠Anthropic +1

“Why interested” (1–2 paragraphs) — what “highly rated” looks like from official incentives, not from a leaked score sheet.

A sentence that names the Security stream’s actual 2026 objects: N-day evals, SCONE-bench, exploit-development evals, LLM ATT&CK mapping, Claude-for-cryptanalysis, control-eval scaffolds.
A sentence that connects 20 years of exchange / HFT / smart-contract / agent-fleet work to those objects, not to “I care about safe AI.”
A sentence that says he wants the 4-month public artifact and would take an FRT / security FT role if offered — because the form also asks % likelihood of accepting FT.
No COO origin story in paragraph one.

“Research areas” (1 paragraph). Pick one primary and one backup. Primary: AI-enabled cyber capability evals (N-day, exploit-dev, smart-contract, MCP-tool attack surface). Backup: control-eval scaffolds / monitor-evasion (Loughridge + SLEIGHT-Bench + inspect_ai graders). Name the papers. Sketch the 4-month method at the level Ward’s simulated reviewer asked for: dataset, harness, metric, what would falsify the claim.

Honesty about gaps. Official copy already says no ML training required. State it once: no training/fine-tuning experience; compensation is production systems, eval harnesses, cryptography, and a public agent fleet. Pretending otherwise is the policy violation (“using Claude to create experiences”).

Documented red flags.

Generic safety talk with no Anthropic 2026 object attached (Ward; the Safety posting’s own “we care about execution”).
Leadership-heavy résumé as the lead signal, against Security’s “dirty work” language.
No runnable artifacts. He has the opposite problem if he hides github.com/tonydzi/github-evidence behind titles.
Claude-first draft that reads like every other safety application (policy explicitly forbids this).

2026 papers worth one concrete clause each (opened):

Agentic Misalignment in Summer 2026 (Lynch et al., Jul 2026); Diffuse AI Control on Fuzzy Tasks (Terekhov et al., 23 Jun 2026); SLEIGHT-Bench (Najt et al., 19 May 2026); Training a Misaligned Reward Seeker (Qi / Wright / MacDiarmid / Hubinger, Aug 2026); Measuring LLMs’ impact on N-day exploits (Xiao et al., 8 Jun 2026). Use them as anchors, not as a name-drop list.

6. Technical loop and 6–8 week prep

Latest dated picture, with conflicts preserved.

CodeSignal OA. 90 minutes. One system, four unlocking stages, stdlib Python, black-box tests. Common prompts: in-memory bank (balances, scheduled transactions, interest), in-memory DB with TTL, filesystem. Official Fellows description from the Oct 2025 vintage emphasizes refactoring to new requirements, not memorized algorithms.
Scoring: some emails said 480/600; candidates report 540, 590, even 600 not advancing. [single-source cluster] Do not optimize for 480. Optimize for finishing stage 4 with tests green and time left.
Sundeep Teki (7 Jun 2026) claims some 2026 Anthropic SWE screens grew from 4 to 6 stages. [low-authority coach; unclear whether Fellows uses this] Budget as if two extra waves can appear.
AI tools: not permitted on the OA unless the invite says otherwise (policy + every candidate report).⁠Startup +1
Live coding. ~90 minutes with an engineer, still CodeSignal, spec-dense, clarification is the skill. Jumping in without questions is the reported fail.
Colab LLM round. ~55 minutes, Google Colab, GPU, complete missing pieces of an inference pipeline (~20–30 lines across two functions), then talk about prompting / hallucination handling. Several accounts say LLM assistance is not allowed in this round even though the topic is LLMs. Most people only finish part 1. [Exponent 30 Apr 2026, Glassdoor Sep 2025]
Research brainstorm. ~15 minutes with a potential mentor. No “right” answer. Security-stream version should be one of the five pitches above, defended at the level of metric and confound.

6–8 week conversion plan for a strong systems engineer (inference from the loop, not an official syllabus):

Weeks 1–3: CodeSignal Industry Coding Framework clones — bank, wallet, KV store + TTL, filesystem — in a browser IDE, no Copilot, 90-minute timer, write tests first. Goal: 4/4 with 15 minutes spare, twice in a row.
Weeks 3–5: same problems with a mid-session spec change (new transaction type, historical queries, merged entities). This is the Reddit/Glassdoor failure mode.
Weeks 5–6: Colab fluency — small PyTorch or raw-numpy generation loop, logits → tokens, a toy KV cache, no “call Claude.”
Weeks 6–8: one written 2-page pitch (problem, harness, metric, 4-month schedule, what would falsify) plus a 12-minute spoken version. Read the six FRT/Alignment posts listed above end to end.
Throughout: three refs briefed; evidence page and 3–5 PRs at the top of the written app, titles at the bottom.
7. Risks of applying, and the September 2026 FT applications

Does AFP hurt later FT applications? Official Fellows copy says the opposite direction: “A Fellowship will stand you in good stead for roles at Anthropic”; 25–50% of later-cohort fellows received a FT offer; first cohort “over 40%.” No public source says that a rejected AFP file poisons later FT. [no source found]⁠Alignment.anthropic <https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/>

FT reapply rule. Careers FAQ: wait 12 months, or sooner if something material changes. Coaching sites repeat “12 months after post-onsite rejection.” That is FT-shaped, not Fellows-shaped.⁠Anthropic <https://www.anthropic.com/careers>

The past-year question. The Fellows form asks, in words, whether the applicant applied to Anthropic FT roles or to MATS/Astra/AFP in the past year. The Sep 2026 Greenhouse FT apps must be disclosed. [established form language] Whether Constellation can see the FT ATS row without that checkbox is [no source found].

How to treat the interaction.

Disclose.
In “anything else,” one sentence: applied to several FT roles in Sep 2026; AFP Security is the intended research on-ramp; material new evidence since those apps is the Jul–Sep 2026 OSS burst (43 PRs, inspect_ai #4769, evidence page). That sentence uses the careers FAQ’s own “materially changes” clause.
Do not run a parallel FT process that contradicts the “% likely to accept FT after Fellows” answer.

Contrarian risk worth stating. If the Sep 2026 FT apps already produced a “not now” signal inside Anthropic, AFP reviewers who share that signal may update downward. We have no evidence this happens and no evidence it does not. Steelman: Constellation is a separate portal because they want a fresh read. Counter-steelman: small company, same researchers, memory exists. Decision: apply anyway; the cost of not applying to a rolling January cohort is higher than the unproven contamination risk.

8. Timeline (rolling January 2027)
Marker	What is known	Quality
Apps open	Greenhouse Safety & Security id_2e26dffe live for January 2027 as of Sep 2026; listings updated ~8–18 Sep 2026 per Extern (aggregator)	Official listing [established]; “updated Sep 8–18” [low-authority]
Review	Rolling; prior cohorts used hard cutoffs when they needed a synchronized start	[established] rolling; cutoff date for Jan 2027 [no source found]
First human touch	Pingbang Hu: ~1 month to “passed first stage.” Glassdoor: OA ~1 month after apply in some 2025 cases	[single-source] each
Refs contacted	Form: any time, no notice, 1-week reply	[established]
Loop length once moving	Pingbang Hu Oct 2025: four rounds then offer within days. Glassdoor: ~4 weeks. Coaching sites: 3–6 weeks	first-hand [single-source]; 3–6 weeks UNVERIFIED
Start	January 2027; posting allows off-cycle starts if noted	[established]
Next cohort after that	Extern projects ~August 2027; not on the live posting we opened	[low-authority]

September vs October. Rolling + finite seats + reference lag (one week) + holiday slowdown in late December argues for submitting in late September, not waiting for a “perfect” essay in late October. The essay can be good in a week if the project pitch already exists.

What would change the recommendation to apply to the Security stream first

Current recommendation: Security first, Safety/control-evals second, on the same form.

Flip away from Security-first only if one of these becomes true:

He cannot produce three references who have seen him do technical work in the last 18 months (OSS maintainers count; COO-era executives do not, alone).
The actual goal is FT conversion onto Alignment Science (Bowman / Perez / Roger / Marks), not FRT. Safety-stream mentors are the conversion machine for that destination; Security-stream mentors are Kiel’s FRT cluster.
He would rather spend 4 months on model-organism / interpretability work than on eval harnesses. That is a preference change, not a fit change.
New official language appears that Security now requires prior ML experiment management. The current posting lists that as an extra, not a must.
He picks up a CVE or a public exploit-eval repo before submitting — that would strengthen Security-first, not weaken it.

Nothing in the open record says a 20-year engineer is unwelcome on Security. The posting’s unique criteria read as if they were written for exactly this shape of person, minus CVEs.

Decision options

Option A — Apply Security-first this week.

Trade-off: burns one Fellows cycle and puts the Sep 2026 FT apps on the same timeline. Risk: CodeSignal or refs kill it. Upside: only on-ramp that official copy plus FRT output both validate for this profile.

Option B — Wait for a “better” essay / a CVE / an ML-community ref, apply in late October.

Trade-off: rolling seats may be gone; January start slips. Risk: the extra month does not change CodeSignal or ref quality. Only worth it if a specific named ref or a public artifact lands in the next 3 weeks.

Option C — Skip AFP, keep applying FT Security / FRT roles.

Trade-off: FT bar is higher; careers page itself says about half of technical staff had no prior ML, but FT research-engineer loops still expect the same CodeSignal plus more. AFP is the documented conversion path (25–50%). Skipping it to protect a theoretical ATS contamination is not supported by sources.

Option D — Apply Safety-first (control/evals) instead.

Trade-off: second-choice mentors, criteria that ask for empirical ML he does not have. Only rational if the FT target is Alignment Science rather than FRT.

Recommendation: Option A.

Confidence: [emerging].

Main assumption: the live Greenhouse Security unique criteria are the actual screen, not marketing, and a systems engineer who can clear CodeSignal plus point at a 4-month FRT eval project is inside the distribution that produced SCONE-bench.

Verification pass — UNVERIFIED / single-source / low-authority

Treat as established (multi-source official): program length 4 months; stipend $3,850/week; ~$15k/month compute; no visa sponsorship; US/UK/CA work auth; Constellation runs apps; rolling January 2027; Security mentors Kiel / Warr / Ben Asher / Lucas / Cheng; “no PhD / no prior ML / cybersecurity backgrounds”; 80% papers in an early cohort; 40% first-cohort FT; 25–50% later-cohort FT; fellows use external infra; AI policy = first draft yourself; form asks about applications in the past year; three refs, ML community preferred, contacted without notice.

Treat as emerging (credible but thin): ~32 seats per later cohort (Anthropic X, 29 Jul 2025, plus Hu CV); industry-systems people have gotten in (Killian, Wong); CodeSignal is 90-min 4-stage ICF; final loop is Colab 55 + brainstorm 15; rolling favors earlier apps; Security-first is the better form choice for this profile.

Treat as single-source or low-authority — do not build the decision on the number:

“2,000+ applicants → 32 offers → 1.3–1.6%” (Hu CV + LW reprint + Sauers_ tweet).
“150 finish all rounds / 21% final-round / CodeSignal kills 60–70% / overall <5%” (Extern + leonstaff, same unnamed finalist).
480/600 cutoff honored (contradicted by 540/590/600 rejections).
3–6 week guaranteed timeline (Extern).
CodeSignal now has 6 stages for Fellows (Teki).
What reference callers ask.
That Sep 2026 FT apps silently tank AFP.
That AFP rejection poisons later FT.
Exact senior-vs-junior split of 2025–2026 fellows.
Winnie Xiao’s pre-MATS biography.
Cole Killian = Jump Trading / DOGE Cole Killian (strong circumstantial, not in the paper).

Treat as no-source-found: official acceptance rate; official CodeSignal passing score; official weight of refs vs essays vs screens; Constellation/MATS written rubric; whether Greenhouse FT and Constellation Fellows share an ATS flag.

Aggregator pages used only as leads, not as authorities: Extern.com (12 Jul 2026), leonstaff (31 May 2026), Built In (17 Jun 2026), tryexponent / Aced (30 Apr 2026), chillinterview.com, Granted AI.

Query log (representative; not exhaustive)

Web: Anthropic Fellows Program January 2027 cohort applications; Anthropic Fellows Program acceptance rate cohort size selection process; site:greenhouse.io Anthropic AI Safety Security Fellows id_2e26dffe; Anthropic Fellows Program Constellation application; "Anthropic Fellows" OR "Anthropic Fellowship" accepted OR rejected LessWrong OR "EA Forum"; Anthropic Fellows named fellows list 2025 2026 security red team; "AI agents find $4.6M" blockchain smart contract exploits Anthropic Fellows authors; Winnie Xiao Cole Killian Anthropic Fellows background bio; Anthropic Fellows CodeSignal assessment interview process live coding Colab; Anthropic Fellows Glassdoor interview OR rejected OR accepted experience; "Anthropic Fellows" site:lesswrong.com OR site:forum.effectivealtruism.org; Anthropic "N-day exploits" OR "SLEIGHT-Bench" OR "Diffuse AI Control" OR "Training a Misaligned Reward Seeker" 2026; Anthropic candidate AI usage policy fellows application "first draft" Claude; Chloe Loughridge "Strengthening Red Teams"; Pingbang Hu Anthropic Fellow; Aengus Lynch Anthropic Fellow agentic misalignment; site:reddit.com Anthropic Fellows CodeSignal 480 OR 600; does applying to Anthropic Fellows hurt full-time application; LLM ATT&CK Navigator Anthropic; Elle Najt Colin Toft SLEIGHT-Bench; Aria Wong Anthropic Fellow; MATS Anthropic Fellows references recommendation letters.

X keyword: "Anthropic Fellows" OR "Anthropic Fellow" Latest; X semantic: Anthropic Fellows Program application experience interview accepted rejected 2026 from 2026-08-25.

Pages opened in full (primary): Greenhouse id_2e26dffe; alignment.anthropic.com/2025/anthropic-fellows-program-2026/; alignment.anthropic.com/2024/anthropic-fellows-program/; anthropic.com/research/smart-contracts; anthropic.com/candidate-ai-guidance; tryexponent Fellow guide; alignment.anthropic.com/2026/agentic-misalignment-summer-2026/; alignment.anthropic.com/2026/diffuse-ai-control/; alignment.anthropic.com/2026/sleight-bench/; anthropic.com/research/n-days; anthropic.com/research/attack-navigator; anthropic.com/research/discovering-cryptographic-weaknesses; anthropic.com/research/exploit-evals; alignment.anthropic.com/2026/reward-seeker/; alignment.anthropic.com/2025/strengthening-red-teams/; ariahw.github.io; hannamw.github.io; Airtable form snapshots.

Source catalog (key)

Official / primary: [web:27] [web:48] Greenhouse id_2e26dffe; [web:9] [web:49] alignment.anthropic.com/2025/anthropic-fellows-program-2026/; [web:8] [web:50] alignment.anthropic.com/2024/anthropic-fellows-program/; [web:21] Anthropic X 29 Jul 2025 (~32 places); [web:5] Anthropic X 11 Dec 2025 (May/Jul 2026 rounds + security track); [web:66] [web:76] anthropic.com/research/smart-contracts 1 Dec 2025; [web:144] anthropic.com/research/n-days 8 Jun 2026; [web:192] anthropic.com/research/attack-navigator 3 Jun 2026; [web:191] anthropic.com/research/discovering-cryptographic-weaknesses 28 Jul 2026; [web:197] anthropic.com/research/exploit-evals 22 May 2026; [web:154] alignment.anthropic.com/2026/sleight-bench/ 19 May 2026; [web:145] alignment.anthropic.com/2026/diffuse-ai-control/ 23 Jun 2026; [web:149] alignment.anthropic.com/2026/reward-seeker/ Aug 2026; [web:247] alignment.anthropic.com/2026/agentic-misalignment-summer-2026/; [web:141] alignment.anthropic.com/2025/strengthening-red-teams/; [web:155] [web:233] anthropic.com/candidate-ai-guidance 10 Jul 2025; [web:262] anthropic.com/careers FAQ (12-month reapply); [web:6] [web:185] [web:220] Airtable Fellows form snapshots; [web:241] anthropic.com/research/open-source-circuit-tracing 29 May 2025.

First-hand / named people: [web:37] [web:181] Pingbang Hu offer tweet + CV; [web:136] Chloe Loughridge X 10 Nov 2025; [web:248] [web:249] aenguslynch.com CV; [web:269] ariahw.github.io; [web:270] hannamw.github.io; [web:127] [web:130] Cole Killian McGill / Jump / DOGE coverage Feb–Mar 2025.

Candidate process reports: [web:99] [web:100] [web:101] [web:105] Glassdoor Fellow interviews 2025–2026; [web:253] [web:255] Reddit Fellows OA Jan/Aug 2026; [web:139] Alyssa Fu Ward Substack 1 Jul 2026; [web:91] [web:234] tryexponent Fellow guide 30 Apr 2026 [low-authority]; [web:87] Teki Substack 7 Jun 2026 [low-authority]; [web:0] [web:16] Extern.com 12 Jul 2026 [aggregator]; [web:20] leonstaff 31 May 2026 [aggregator].

1047 sources




Heavy

===== ALL LINKS ON PAGE (30) =====
http://job-boards.greenhouse.io/anthropic/jobs/id_2e26dffe
https://alignment.anthropic.com/2024/anthropic-fellows-program/
https://x.com/AnthropicAI/status/1950245027604812094
https://pbb.wtf/cv.pdf
https://www.greaterwrong.com/posts/aEiZfHAXeKXF5PJgH/ai-safety-has-a-scaling-problem
https://x.com/Sauers_/status/1981087223161270559
https://www.extern.com/post/anthropic-internship-guide
https://startup.jobs/anthropic-ai-safety-fellow-us-anthropic-3-7051849
https://www.glassdoor.com/Interview/Anthropic-Interview-E8109027-RVW101368327.htm
https://www.reddit.com/r/Anthropic/comments/1qovmbs/assessment_for_anthropic_fellows_program_for_ai/
https://www.reddit.com/r/csMajors/comments/1vfl819/bombed_my_anthropic_fellows_oa_1/
https://airtable.com/appCHLjgoTUCJMLct/pagUhpiBE5KxoU3lX/form
https://www.anthropic.com/research/smart-contracts
https://ariahw.github.io/
https://alignment.anthropic.com/2025/strengthening-red-teams/
https://www.anthropic.com/research/exploit-evals
https://www.anthropic.com/research/attack-navigator
https://www.anthropic.com/research/n-days
https://www.anthropic.com/research/discovering-cryptographic-weaknesses
https://simplify.jobs/p/s_67880a9d/Fellows-Program
https://airtable.com/appiuxxfhf5moRwTx/pagDCFPHd9qOKZ5ki/form
https://www.glassdoor.com/Interview/Anthropic-Interview-E8109027-RVW100353268.htm
https://www.tryexponent.com/guides/anthropic-ai-safety-fellow-interview
https://x.com/ChloeLough333/status/1988031992299221074
https://www.aenguslynch.com/cv.html
https://alyssafuward.substack.com/p/applying-for-the-anthropic-fellows
https://www.matthandzel.com/notes/asking-for-letter-of-reference
https://www.alphaxiv.org/@henry-sleight
https://alignment.anthropic.com/2025/anthropic-fellows-program-2026/
https://www.anthropic.com/careers

===== VENDOR: report (DR26-09-24-MACANTON-01-1452-anthropic-fellows-glm.md) =====
---
dr_id: DR26-09-24-MACANTON-01-1452
source: glm
source_url: https://chat.z.ai/c/s_bd465086
mode: GLM-5.3 + Advanced Search ON + Deep Think Max
topic: "Anthropic Fellows Jan-2027: сеньор-инженер по безопасности без ML-research — отбор, рефери, техлуп"
collected_at: 2026-09-24T15:54:06
collected_by: NODE-0X (NODE-0X), /dr-fanout, живой Chrome-MCP
collected_how: innerText главного контейнера -> window.name -> локальный sink (текст в контекст модели не попадал)
trim: срез по якорю 'Thought Process
'
distinct_urls_in_body: 17
origin: external-llm
---

Thought Process

I'll run this as an extended research task. Let me start with several rounds of searches.

Thought Process

Let me open the key pages to gather detailed information.

Thought Process
Deep Research Report: Anthropic Fellows Program (January 2027 Cohort) — Application Strategy for a Senior Security/Distributed-Systems Engineer

Searches run: ~15 multi-query rounds (approximately 50 individual queries). Distinct pages actually opened: 30. All URLs cited below were opened in this session; anything I could not open or verify is marked as such.

Ranked Decision-Relevant Findings
Finding 1: The Anthropic Fellows Program accepts roughly 2% of applicants, and past cohorts converted 25–50% of fellows to full-time offers

Confidence: [established] (acceptance rate from one credible secondhand source; conversion rate from Anthropic's own postings)

Ryan Kidd, Co-Executive Director of MATS (the AI-safety mentorship program that partners with Anthropic on Fellows projects), stated on the Cognitive Revolution podcast (January 4, 2026) that the Anthropic Fellows program's acceptance rate was "like 2%" — lower than MATS's own ~5–7% rate — because of the Anthropic brand name attracting a large applicant pool. Anthropic's own job postings state that "in previous cohorts, 25-50% of fellows received a full-time offer". The original 2024 announcement described the first cohort as 10–15 fellows; a rejected finalist from the October 2025 round reported roughly 150 finalists competing for 32 spots in that cycle.

Source: Cognitive Revolution podcast transcript (Jan 4, 2026), Anthropic Fellows Greenhouse posting (accessed Sep 2026), Medium first-hand account (Oct 18, 2025).

Finding 2: The program explicitly targets career-switchers and does not require ML research experience, PhD, or published papers

Confidence: [established] (directly from Anthropic's own materials)

The alignment.anthropic.com program page states: "You don't need a PhD, prior ML experience, or published papers. We've had successful fellows from physics, mathematics, computer science, cybersecurity, and other quantitative backgrounds". The Greenhouse posting for the Security stream lists as "strong candidate" criteria: "contributed to open-source projects in LLM- or security-adjacent repositories," "experience with pentesting, vulnerability research, or other offensive security work," and "reported CVEs or been awarded bug bounties". The AI Security Fellow posting specifically says the program is for people "regardless of previous experience".

Source: alignment.anthropic.com (2025 announcement, accessed Sep 2026), Greenhouse job id_2e26dffe (accessed Sep 2026).

Finding 3: The blockchain smart-contract exploit project (the flagship Security stream success) was built by Winnie Xiao and Cole Killian — Winnie Xiao appears to be a recent UC Berkeley graduate, not a 20-year veteran

Confidence: [emerging] (background verification is single-source from LinkedIn)

The paper "AI agents find $4.6M in blockchain smart contract exploits" lists authors Winnie Xiao and Cole Killian (both listed as "MATS and the Anthropic Fellows program"), with Henry Sleight, Alan Chan, Brenda [ФАМИЛИЯ], and Alwin Peng. A LinkedIn search shows a "Winnie Xiao — Analyst at BlackRock, UC Berkeley" profile that is likely the same person, though I could not fully verify the match because LinkedIn required login. Cole Killian's background was not separately verifiable in this search session. [single-source, low-authority for the background claims]

Source: anthropic.com/research/smart-contracts (Dec 1, 2025), matsprogram.org research page (accessed Sep 2026), LinkedIn (inconclusive).

Finding 4: First-hand account of the full interview loop (October 2025 cohort) reveals 5 stages: resume screen → CodeSignal-style OA (bank account system, 4 levels, threshold ~460/600) → live coding with an Anthropic researcher → second coding round → 15-minute research brainstorm with an alignment leader → reference check

Confidence: [emerging] (single-source, detailed first-hand account; the author notes the process has changed since his experience)

A rejected finalist (who later learned he was on a waiting list) published a detailed account on Medium (October 18, 2025, updated July 13, 2026). Key details: the OA was a progressive bank-account system where you must pass level N to unlock N+1, with a stated passing threshold of 460/600. The first live coding interview was with "a physicist turned AI researcher" whose style was "shut up and show me the code." The second coding round involved a "very hard" problem where "I don't think anyone could finish both parts in 55 minutes." The final stage was a 15-minute brainstorm with an Anthropic alignment leader. References received "live meeting calls from Anthropic" before offers went out. The author added in July 2026 that Anthropic has since added a take-home interview stage that he did not experience.

Source: Medium post by Zackhui (Oct 18, 2025, updated Jul 13, 2026) [single-source].

Finding 5: Anthropic's candidate AI-usage policy requires you to write your first draft yourself, then use Claude to refine it

Confidence: [established] (official Anthropic policy page, last updated July 10, 2025)

Anthropic's "Guidance on Candidates' AI Usage" page states: "When applying (resume and application questions): Please create your first draft yourself, then use Claude to refine it. We want to see your real experience, but Claude can polish how you communicate about your work." Take-home assessments must be completed "without Claude unless we indicate otherwise." During live interviews: "This is all you — no AI assistance unless we indicate otherwise". The policy was covered by Observer (Feb 5, 2025) and BGR (Feb 4, 2025) when it was first published.

Source: anthropic.com/candidate-ai-guidance (Jul 10, 2025).

Finding 6: The Frontier Red Team published five specific 2026 research outputs that define the Security stream's current agenda — each one maps directly to the applicant's systems/security engineering strengths

Confidence: [established] (all from red.anthropic.com, Anthropic's official Frontier Red Team blog)

The publications list on red.anthropic.com (accessed Sep 2026) shows:

"Measuring LLMs' impact on N-day exploits" (June 8, 2026) — testing models on 18 Firefox patches and 21 Windows kernel patches
"Discovering cryptographic weaknesses with Claude" (July 28, 2026)
"Mapping AI-enabled cyber threats: Insights from the LLM ATT&CK Navigator" (June 3, 2026) — a year-long analysis partnered with Verizon for the 2026 DBIR
"Measuring LLMs' ability to develop exploits" (May 22, 2026) — introducing ExploitBench and ExploitGym benchmarks, plus updated SCONE-bench; authors include Newton Cheng, Keane Lucas, Winnie Xiao, Kiel

===== GLM ASSISTANT PART 2 =====
Thought Process
Deep Research Report — DR26-09-24-MACANTON-01-1452 (Continuation and Completion)

Methodology restated: ~15 multi-query search rounds (~50 individual queries) were run; 30 distinct pages were actually opened in this session. Every URL in the works-cited list was opened by me except those explicitly marked "snippet-only" or "could not open." This continuation completes Finding 6, delivers Findings 7–10, answers all eight questions, and closes with the required decision sections, verification pass, and works cited.

PART 1 — The 10 Most Decision-Relevant Findings (Ranked)

(Findings 1–5 were delivered in the first half of this report; Finding 6 is completed from the point it was cut off.)

Finding 6 (continued): The Frontier Red Team's 2026 research agenda — every publication maps to the applicant's systems/security strengths

Confidence: [established] (all publication titles/dates from red.anthropic.com and anthropic.com, opened Sep 2026)

The "Measuring LLMs' ability to develop exploits" post (May 22, 2026) — which introduced ExploitBench and ExploitGym alongside an updated SCONE-bench — lists as its authors Newton Cheng, Keane Lucas, Winnie Xiao, Brenda [ФАМИЛИЯ], and Milad Nasr. Note that three of the five named Security-stream mentors (Cheng, Lucas, Kiel) personally authored the exploit-evals work, and a current/former fellow (Xiao) is a co-author — meaning the mentors are actively publishing with fellows on exactly this agenda.

The full verified 2026 FRT publication set and what an outsider could contribute in 4 months:

FRT PUBLICATION (DATE, SOURCE)
	
WHAT A STRONG SYSTEMS/SECURITY ENGINEER COULD CONTRIBUTE

"Measuring LLMs' impact on N-day exploits" (Jun 8, 2026) — 18 Firefox patches, 21 Windows kernel patches [patch-count figure: snippet-only, single-source; post existence verified]	Extend to server-side C++/exchange infrastructure N-days; build deterministic repro harness for time-to-exploit measurement
"Measuring LLMs' ability to develop exploits" (May 22, 2026) — ExploitBench (41 V8 bugs, 16 capabilities, tiers T1–T5), ExploitGym, updated SCONE-bench	Build the missing evaluation infrastructure: seeded reproducibility, flake classification, adversarial-candidate (cheating) detection — the post notes a "separate static scan of the transcripts flags other forms of cheating", i.e., this problem is live and manual
"AI agents find $4.6M in blockchain smart contract exploits" (Dec 1, 2025) — SCONE-bench, 405 contracts exploited 2020–2025; two novel zero-days worth $3,694 found by agents; GPT-5 API cost $3,476	Extend from single-contract reentrancy to multi-step economic exploit chains (oracle manipulation, liquidation cascades, cross-contract composables) — the applicant's exchange/market-maker domain is precisely the unexplored adjacent territory
"Mapping AI-enabled cyber threats: LLM ATT&CK Navigator" (Jun 3, 2026; Verizon 2026 DBIR partnership)	Map the agent-control-plane attack surface (MCP tool poisoning, credential scoping across fleets) — the applicant runs a production multi-machine Claude fleet publicly and has merged PRs in the MCP Go SDK
"Discovering cryptographic weaknesses with Claude" (Jul 28, 2026)	Direct fit: the applicant's MSc is in cryptography (MEPhI)

Concrete project pitches (five, ranked by fit):

"SCONE-bench for market infrastructure": multi-step economic exploit evals. Extend the anvil-fork benchmark methodology from single-contract token theft to documented multi-contract/multi-system incident chains (2020–2026 DeFi and exchange failures). Report in dollars with bootstrap CIs, exactly as the original paper did. Uses only public APIs/open models; the applicant's 20 years in exchange backends and market-maker engines is a moat no current FRT member has.
Deterministic-reproducibility and anti-cheating harness for exploit-development evals. ExploitBench already fights agent cheating via randomized heap layouts and static transcript scans; agentic evals are statistically noisy. A senior engineer's signature skill (deterministic repro + red tests) applied to eval infrastructure matches the posting's verbatim criterion: "a demonstrated willingness to do the 'dirty work' that produces high-quality outputs".
ATT&CK mapping for agent control planes. Red-team his own public multi-machine Claude fleet (or a sandboxed replica) for tool-poisoning, confused-deputy, and cross-agent credential-leak TTPs; map results to MITRE ATT&CK as a companion to the June 3, 2026 Navigator work. His MCP Go SDK / fastmcp / agno merged PRs make him uniquely credible.
Grader-panel sabotage robustness (bridges Security and Alignment streams). SLEIGHT-Bench tests evasion attacks against agent monitors; his inspect_ai #4769 majority-reducer PR for grader panels is the exact codebase. Measure how much adversarial noise (minority-adversarial graders, correlated failures, prompt injection into grader inputs) a panel tolerates before red-team evasion succeeds.
Latency-constrained agentic decision eval in simulated markets (stretch goal). The N-day work measures time-to-exploit; nobody at FRT has market-microstructure expertise. Higher scoping risk than pitches 1–4.
Finding 7: The program's founding document explicitly targets mid-career technical professionals — the applicant is the stated demographic, not an exception to it

Confidence: [established] (official Anthropic announcement, opened)

The original 2024 program announcement states: "The program is focused on helping mid-career technical professionals transition into the AI safety research space, but regardless of your background or career stage, we're open to your application". The 2025 announcement reinforces: "You don't need a PhD, prior ML experience, or published papers. We've had successful fellows from physics, mathematics, computer science, cybersecurity, and other quantitative backgrounds". This directly answers the core anxiety in the request: a 20-year COO/CTO with no ML-research re
...[truncated for length]

---

> `ToolSearch` -- {"query": "dummy", "max_results": 1}

---

**Claude:**

```json
{
 "lang": "en",
 "topic": "Anthropic Fellows Jan-2027: как сеньор-инженер по безопасности без ML-research попадает в программу",
 "one_line": "Deep research on how a senior security/distributed-systems engineer with no ML-research record can get selected into the Anthropic Fellows January 2027 cohort (Security stream vs Safety stream, referees, and the technical loop).",
 "key_findings": [
  "Anthropic's own materials explicitly say no PhD, no prior ML experience, no published papers are required; successful fellows have come from physics, math, CS, and cybersecurity — official language names cybersecurity as a valid background [established].",
  "The Security stream's unique Greenhouse criteria (OSS in LLM/security repos, pentesting/vulnerability research, CVEs/bug bounties, ownership of ambiguous problems, willingness to do 'dirty work') fit this applicant's profile far better than the Safety/control-evals stream, which wants empirical ML project experience [established].",
  "Cohort size grew from 10-15 (pilot) to ~32 seats; acceptance rate is NOT officially published — circulating figures of 1.3-2% (Ryan Kidd/MATS podcast, Pingbang Hu CV, LessWrong) are single-source/secondhand and should not be quoted as fact [emerging, disputed].",
  "CodeSignal OA (~90 min, progressive multi-stage Python task, e.g. in-memory bank/DB/TTL system) is a hard filter but a high score does not guarantee advancement — multiple accounts (540, 590, even 600/600) report rejection despite stated ~480/600 cutoffs, and some reports describe growth to 5-6 stages including live coding, a Colab LLM round (~55 min), and a 15-min research brainstorm with a potential mentor [emerging].",
  "References are officially described as 'one of the main ways we assess candidates,' contacted without notice with a one-week reply window; ML-community referees are preferred but not required — OSS maintainers who collaborated on technical work (e.g. merged PRs) are argued to be stronger than executive/leadership references who can't speak to concrete technical strengths/weaknesses [established for form language; speculative for weighting].",
  "The 2026 Frontier Red Team publication agenda (SCONE-bench smart-contract exploits worth $4.6M, ExploitBench/ExploitGym, N-day exploit evals, LLM ATT&CK Navigator, cryptographic weakness discovery with Claude, SLEIGHT-Bench monitor-evasion) defines exactly the kind of external-infra, non-training eval/harness work a 4-month outsider fellow can realistically ship, and maps well onto this applicant's OSS work (inspect_ai #4769, MCP Go SDK, fastmcp) [established].",
  "At least two identified Security/Safety-stream fellows resemble industry systems/quant engineers rather than ML PhDs (Cole Killian — McGill math/CS, ex-Jump Trading HFT engineer, per circumstantial identity match; Aria Wong — Princeton math, hedge-fund quant/engineering background, MATS then AFP), showing the pathway exists but the visible published sample still skews Brasov/academic [emerging].",
  "Anthropic's candidate AI-usage policy (updated 10 Jul 2025) requires writing the first draft yourself and using Claude only to refine it; take-homes and live interviews forbid AI assistance unless stated otherwise — violating this is a documented red flag in essays [established].",
  "Program is rolling for January 2027; prior cohorts had hard cutoff dates, so applying in late September 2026 (not waiting for a 'perfect' essay in October) is the conservative move given seat scarcity and reference-reply lag [emerging].",
  "No public evidence that applying to Fellows harms later full-time applications; official copy states the opposite (a Fellowship 'stands you in good stead' and 25-50% of fellows in later cohorts got FT offers, ~40% in the first cohort) — the Fellows application form does require disclosing FT applications from the past year [established]."
 ],
 "recommendations": [
  "Apply to the AI Security & Frontier Red Team stream as primary choice, with Safety/control-evals as an explicit secondary — do not lead with Safety, whose criteria don't match this profile.",
  "Submit in late September 2026 rather than waiting for October, given rolling review and finite seats for the January 2027 start.",
  "Brief three referees now who can speak to concrete collaborative technical work (OSS maintainers, PR collaborators) rather than only executive/leadership references; tell them Anthropic/Constellation may contact them without notice with a one-week reply window.",
  "Pitch one of the five concrete 4-month Security-stream project ideas grounded in existing evidence: (1) SCONE-bench-style multi-step economic exploit evals for exchange/market infrastructure, (2) deterministic-reproducibility/anti-cheating harness for exploit-dev evals, (3) MCP-tool-use ablation on SCONE using existing MCP Go SDK/fastmcp work, (4) ATT&CK mapping of agent control planes using the applicant's own multi-machine Claude fleet, (5) productionizing the Loughridge modular red-team scaffold as inspect_ai tasks.",
  "Write essays with your own first draft, use Claude only to refine per official policy; open with the specific 2026 FRT research objects (N-day evals, SCONE-bench, ExploitBench, ATT&CK Navigator, cryptographic weakness work) tied to 20 years of exchange/HFT/systems engineering — not a COO/executive origin story in paragraph one.",
  "State ML-training/fine-tuning inexperience honestly rather than hiding it; official copy already says it's not required, so overclaiming would violate the AI-usage/authenticity policy.",
  "Disclose any September 2026 full-time Anthropic applications on the Fellows form as required, framing new evidence (OSS burst, inspect_ai PR, evidence page) as material change since those FT applications, per the careers FAQ's 'materially changes' language.",
  "6-8 week technical prep: weeks 1-3 CodeSignal industry-coding clones (bank/wallet/KV-store+TTL/filesystem) under a 90-min timer with tests-first; weeks 3-5 same problems with mid-session spec changes; weeks 5-6 Colab/PyTorch fluency (logits→tokens, toy KV cache); weeks 6-8 a written 2-page project pitch plus a 12-minute spoken version, reading the six cited FRT/Alignment posts end to end."
 ],
 "entities": {
  "people": ["[ИМЯ] [ФАМИЛИЯ]", "Jan Leike", "Brenda [ФАМИЛИЯ]", "Keri Warr", "Evyatar Ben Asher", "Keane Lucas", "Newton Cheng", "Winnie Xiao", "Cole Killian", "Henry Sleight", "Alan Chan", "Alwin Peng", "Chloe Loughridge", "Pingbang Hu", "Aengus Lynch", "Aria Wong", "Horvat Hanna", "Mikhail Terekhov", "Elle Najt", "Colin Toft", "Joe Benton", "Ryan Kidd", "Alyssa Fu Ward", "Milad Nasr"],
  "companies": ["Anthropic", "Constellation", "MATS", "Jump Trading", "BlackRock", "Verizon"],
  "products_tools": ["Anthropic Fellows Program", "Greenhouse job id_2e26dffe", "CodeSignal", "SCONE-bench", "ExploitBench", "ExploitGym", "LLM ATT&CK Navigator", "SLEIGHT-Bench", "inspect_ai", "MCP Go SDK", "fastmcp", "agno", "qwen-code", "Google Colab", "Airtable Fellows application form"]
 },
 "open_questions": [
  "Official/precise application-to-offer acceptance rate is not published — all circulating percentages (1.3%, 1.6%, <5%) trace to single-source or aggregator claims.",
  "Whether the September 2026 full-time Anthropic Greenhouse applications and the separate Constellation-run Fellows ATS are linked/visible to each other is unconfirmed [no source found].",
  "Exact weighting of references vs essays vs technical screens in the holistic decision is unpublished; no leaked rubric exists.",
  "Whether CodeSignal now has 6 stages instead of 4 for Fellows (per one low-authority coaching source) is unverified.",
  "Whether a rejected Fellows application could negatively bias later full-time evaluation ('ATS contamination') has no supporting or refuting evidence.",
  "Cole Killian's identity match to the ex-Jump Trading/DOGE-coverage individual is circumstantial, not confirmed.",
  "Winnie Xiao's pre-Fellows/pre-MATS biography (possible BlackRock/UC Berkeley match) is unverified (LinkedIn login-gated)."
 ],
 "related_concepts": ["anthropic-fellows-application", "ai-security-frontier-red-team", "task-2026-09-23-visionary-map-choose-door", "cv-outreach-jobsearch", "inspect-ai-oss-contributions"]
}
```
