---
session: s_4a7d5e12
date: 2026-10-09
words: 8613
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-09 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4a7d5e12` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-08-ZB-01-1645
REGISTRY TOPIC: Контрибьюторы на GitHub tonydzi: как превратить соло-портфель агентных и second-brain репо в комьюнити Palo Alto AI Research Lab (механики привлечения, кейсы Aider/OpenHands/Letta/Khoj/mem0, лаба=комьюнити, метрики, 90-дневный план) (через dr_start; ПОТРЕБИТЕЛЬ: Decision Memo: план первых 5 шагов по привлечению контрибьюторов + аудит репо tonydzi (сессия NODE-0X 08.10 по голосовой оператора 16:35)) (dr_reconcile 2026-10-08: на диске 2/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-10-08-ZB-01-1645\results)

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


===== VENDOR: claudeai (claudeai.md) =====
---
dr: DR26-10-08-ZB-01-1645
rail: claudeai#web
account: a2 (claude.ai web, Max plan, user shown as "Arthur Dzi")
mode: Opus 5.5 Max + Research (Deep research, "Research complete • 276 sources • 6m 14s")
chat: https://claude.ai/chat/s_ae0da8a9
sent: 2026-10-08 16:48 PDT
collected: 2026-10-08 17:03 PDT
collected_by: Claude Code (Fable 5.1) on NODE-0X-2023PAL via local Chrome (Claude-in-Chrome MCP), page DOM innerText of the artifact + 64 unique hrefs
Machine: NODE-0X-2023PAL · Agent: Claude Code · Operator: dev · 2026-10-08
---

# From a solo agent fleet to a contributor lab: what the 2025–2026 evidence says, and a 90-day plan for tonydzi / Palo Alto AI Research Lab

Your contributor problem is not visibility. It is responsiveness and trust. 7 of your 15 external PRs never got a human reply. In the research and CHAOSS literature, slow or missing first responses are the best-documented reason newcomers leave. On top of that, agents posting under your personal account make it impossible for strangers to know when they are talking to you. Fix those two things first, then shrink to 2–3 flagship repos with one public "lab artifact" (a benchmark or eval that people can contribute results to). Do this before any distribution push.

## TL;DR

- Answer every human, fast, as a human. Time-to-first-response is the metric with the strongest evidence for newcomer retention. Your current state (47% of external PRs ignored, 4-day first replies against a promised 48h) is worse than having no promise at all. Close the backlog this week and make a promise you can keep.
- Separate yourself from your agents and disclose them proudly. GitHub's Terms make you responsible for everything posted under your account. GitHub allows one free machine account. Projects like Aider print "Aider wrote X% of the code in this release" and still grew. Disclosure plus human accountability works. Undisclosed agent replies under a person's name do not.
- Become a lab by shipping one shared artifact, not 60 repos. EleutherAI, BigScience and OpenHands all formed around one concrete public goal: replicate GPT-3, train BLOOM, build an open Devin. Pick 2–3 flagships, move them to an org, and build a contributable benchmark around second-brain / agent-memory retrieval.

## Executive summary (10 bullets)

1. Your premise about GitHub is verified. In February 2026 GitHub added settings to disable pull requests entirely or restrict them to collaborators. On June 17, 2026 it added a cap on open PRs from users without write access, with a bypass list. [visualstudiomagazine] Drafts do not count, and PRs opened by Copilot or other AI agents do count. [github] On August 6, 2026 these caps became configurable at the organization level. [github] GitHub also added an option to restrict issue creation to collaborators. [visualstudiomagazine]
2. Many projects now gate PRs on an accepted issue. mem0 auto-closes PRs that do not link an issue with the accepted label, keeps a VOUCHED.td trust list, and says: "Using AI to write code is fine. Most of us do." [github] Ghostty (since January 2026) allows AI-assisted PRs only for accepted issues. [x] Your accepted label is the right idea, but only if a human actually curates it.
3. Good-first-issue labels still work, but they are weaker each year. Hoshikawa, Tanaka, Shimari, Kula and Matsumoto (EASE 2026) studied 406,826 issues and 1,117 newcomer GFI PRs across 37 repos from July 2021 to June 2025. They found that "newcomer engagement with GFI issues remains stable at approximately 27%." Over the same period the share of issues labeled GFI fell from about 0.9% to 0.6%, and "the merge rate of newcomer GFI PRs declined from 61.9% to 42.2%." Mentoring matters more than the label: Tan et al. (ICSE 2023) found "a 71% increase in newcomers' initial contributing success with expert involvement."
4. Bots distort your health metrics. CHAOSS says Time to First Response should count humans only. [chaoss] A 2026 analysis notes that AI triage bots push TTFR "to seconds." [nesbitt] If your agents reply, your dashboard will lie to you.
5. Disclosure is now the norm. Bans exist, but they are the minority. Wenhao Yang, Runzhi He and Minghui Zhou (arXiv, July 2026) coded 455 AI-contribution rules from 102 communities. The rules range from total bans (Zig, QEMU, NetBSD, Gentoo) to disclosure requirements (Linux kernel "Assisted-by", TypeScript, ESLint, MicroPython). [adafruit +2] Their RepoComplianceBench tested four frontier models on 106 issues from 49 repos and found that "today's agents almost never proactively retrieve the contribution rules."
6. Solo-plus-AI projects can grow. Aider's release notes report that "Aider writes most of its own code, usually about 70-80% of the new code in each release." [github] Cline started as a hackathon project that did not place. GitHub's Octoverse 2025 named it "the fastest growing AI-focused open source project and the platform's second fastest growing project overall" (after zen-browser/desktop), with 4,704% year-over-year contributor growth. "Many" of its 35+ staff started as open-source contributors.
7. "Lab" communities formed around one artifact and a public place to work. EleutherAI began as a Discord in July 2020 to replicate GPT-3. Its server "does not strongly differentiate between employees, volunteers, and collaborators." [eleuther] BigScience gathered over 1,000 researchers into 30 self-organized working groups, which grew from 10 initial proposals. [openreview, arxiv]
8. Fragmentation hurts you, and moving to an org is cheap. GitHub transfers keep stars, issues, PRs, watchers and redirects. Redirects break only if you later create a repo at the old path, and GitHub Pages URLs change. [github +2] I found no study proving that orgs increase participation (unverified). The case rests on reduced confusion and on org-level controls such as PR limits.
9. Distribution must be "tryable" and technical. Show HN rules require something people can run. They exclude blog posts and lists, and say "Don't post quickly-generated one-offs." [favors, saascity] r/LocalLLaMA limits self-promotion to about 1/10 of your activity. [intoru] Hacktoberfest 2026 dropped the PR quota because of spam, so it is no longer a contributor pipeline. [dev]
10. Fake stars are a trap. The StarScout study (He, Yang, Burckhardt, Kapravelos, Vasilescu and Kästner; CMU, Socket and NC State) flagged 4.5 million suspected fake stars. After filtering, 3.1 million fake stars from 278,000 accounts across 15,835 repos remained. It also found that "fake stars only have a promotion effect in the short term (i.e., less than two months)" and then "become a burden in the long term." Your honest 53 followers are a better base than any inflated number.

## Per-question findings

### Q1. What converts a stranger into a first-time contributor (2025–2026)?

What has evidence:

- Fast, human first response. CHAOSS defines Time to First Response as a core health metric: "A long delay in response might indicate low community engagement, while a shorter response time can encourage more participation." [chaoss] Its starter health model says the metric applies only to human responses. [chaoss] A study of time-to-first-response in GitHub PRs found that bots often produce the first response and should be analyzed separately from humans. It also found that the human first response strongly shapes PR lifetime. [zenodo, researchgate] A study on PR abandonment found that contributors report long waits for the first review comment as a reason to give up. [github]
- Mentoring on the first task. Tan et al., "Is It Enough to Recommend Tasks to Newcomers? Understanding Mentoring on Good First Issues" (ICSE 2023), found "a 71% increase in newcomers' initial contributing success with expert involvement." Among newcomers who came back, 64.4% had had expert participation on their first issue.
- A curated, well-scoped first task. Hoshikawa et al. (EASE 2026) found that "newcomer engagement with GFI issues remains stable at approximately 27%," while "the merge rate of newcomer GFI PRs declined from 61.9% to 42.2%." The authors recommend "actively creating and labeling GFIs while sustaining review support for newcomer PRs." Newcomers are writing 57% longer PR descriptions, yet merge rates still fell. Effort alone does not convert newcomers if review capacity is missing.

What the case projects show (primary sources where found):

- OpenHands started on March 12, 2024 as a repo that was "still just a README." Early contributors came because the idea (an open-source Devin) was clear and visible. Robert Brennan says he "made one of the first PRs" and found Graham Neubig "in the community Slack pretty quickly." [openhands] By its ICLR 2025 paper it had "more than 2.1K contributions from over 188 contributors." [openreview] Its maintainer ladder: any maintainer can nominate a contributor with "sustained and high-quality contributions," followed by a discussion period of at least 3 days. [openhands]
- Cline says its community "wrote guides that turned newcomers into contributors in hours instead of weeks." It names a contributor, Tomas, who used Cline itself to navigate the repo [cline] and is now on the team. [cline] Rituals: Discord with a #contributors channel, plus r/cline. [github] It has a $1M Open Source Grant program, which is a funded grant, not a per-issue bounty. [ghost]
- Aider takes benchmark results and coding conventions as PRs. [github, aider] That is a low-barrier, high-value contribution type. It requires an Individual Contributor License Agreement. [github]
- mem0 uses: issue first, then the accepted label, then PR. A PR Gate auto-closes the rest ("Closed does not mean rejected"). It also has a "First Contribution Fast Path" for documentation / good first issue, a vouch list, a CLA bot, and GitHub Discussions. [github]
- Continue has a public project board of contribution ideas, a good-first-issue label, GitHub Discussions, and asks contributors to "Open a new issue or comment on an existing one before writing code." [github] Its current README is written in the past tense ("What we built together…"). [github] That may signal a sunset or pivot (unverified).
- SillyTavern sets a soft limit of 200 changed lines per PR and asks contributors to use templates for issues and feature requests. [github, github]
- Letta points to letta-ai/letta-code as the current source. The old repo shows "Only collaborators can create PRs," and its releases auto-credit "New Contributors." [github, github]
- Khoj, crewAI, smolagents, Dataview, Smart Connections, Copilot for Obsidian: rituals beyond "Discord / Discussions / CONTRIBUTING exists" are unverified. Copilot for Obsidian has a Discord for dev discussions, an AGENTS.md, and a paid Plus tier. [github +2]
- How each project got its first 10 external contributors, and its median first-response time: unverified for every project. No primary source states these numbers.

Bottom line for you: strangers convert when (1) the project has one clear, exciting goal, (2) there is a scoped task with context, and (3) a human answers quickly. Bounties are not the common factor. None of the case projects I could verify runs per-issue bounties (for most of them this is "not seen," not "confirmed none").

### Q2. Solo maintainer + agents: disclosure, trust, labeling

- Aider is the model to copy. It is maintained mostly by Paul Gauthier. Every release note states the share of AI-written code, for example "Aider wrote 79% of the code in this release" (v0.84.0). [x] The release-history page states that "Aider writes most of its own code, usually about 70-80% of the new code in each release," based on git history. [github] Disclosure became a feature, not a scandal. Whether it caused contributor growth is unverified.
- Ghostty shows how fast norms changed. In August 2025 it required disclosure. [redmonk] Within weeks, about 50% of PRs carried an AI disclosure (as reported in an interview write-up, secondary). [withstoa] Mitchell Hashimoto's reason: "The disclosure is to help maintainers assess how much attention to give a PR." [specstory] In January 2026 a standalone AI_POLICY.md allowed AI-assisted PRs only for accepted issues and threatened bans for "bad AI drivers." [x, codenote] It also says: "This is not an anti-AI stance. Ghostty is written with plenty of AI assistance." [redmonk] In February 2026 he released Vouch, a trust list where you "get vouched by simply introducing yourself in an issue." [itsfoss] A secondary source reports that Ghostty moved off GitHub in April 2026 (not verified against a primary source). [codenote]
- The range of policies. TypeScript: "If your PR appears AI-authored and you do not include this disclosure, your PR will be closed without review." LangChain's test: "If the effort required to create a pull request is less than the effort required for maintainers to review it, that contribution should not be submitted." [dev] Godot banned autonomous agents and vibe-coded submissions in June 2026. The Linux kernel requires an "Assisted-by:" tag plus human liability. [generativelabs] tldraw auto-closed all external PRs starting January 2026 and called it temporary. [pickuma] Several projects ban AI co-author trailers (reported for Kubernetes, Rust, Node.js; secondary compilation). [dev]
- Agents do not follow these rules on their own. RepoComplianceBench (Yang, He and Zhou, arXiv, July 2026) tested four frontier models on 106 issues from 49 repos. It found that "today's agents almost never proactively retrieve the contribution rules," and that they never refused to contribute to a repo that bans AI. If your fleet contributes to other people's repos, you must enforce their rules in your own harness.
- GitHub's rules on your setup. The Terms say a machine account is "set up by an individual human who accepts the Terms on behalf of the Account… and is responsible for its actions." You may have "no more than one free machine account in addition to your free Personal Account." "You are responsible for all content posted and activity that occurs under your Account." [github] Agents posting as you is not banned. But it mixes your human voice with machine output. A public issue in another organization describes "Agents act on GitHub with the human's identity and full token" as a problem, and proposes GitHub App installation tokens (app[bot] identity, 1-hour scoped tokens) as the fix. [github] One developer reports that a disclosed bot account was hidden by GitHub for a month without notice. [dev] Treat machine accounts as somewhat fragile (single anecdote).

How to label agent activity so humans still engage:

- All agent writing goes through one machine account or a GitHub App, so readers see [bot] or a clear bot name.
- Start each agent-written issue with one line: "Drafted by an agent (model X); reviewed by @tonydzi: yes/no."
- Never let an agent give the first reply to a human's first PR or issue. That reply is yours, even if it is two sentences.
- Add Assisted-by: commit trailers, as the Linux kernel does. Avoid AI "Co-authored-by" trailers, which several projects now reject.

### Q3. "The lab is the community": what made outsiders feel they were joining

- EleutherAI: founded in July 2020 by Connor Leahy, Sid Black and Leo Gao "as a Discord server for people who wanted to replicate GPT-3 in the open." Today it has about 15 staff working "alongside a dozen or so regular volunteers." Its Discord "does not strongly differentiate between employees, volunteers, and collaborators." Note that it "ask[s] that people interested in learning about AI research primarily observe." [eleuther] It added a structured on-ramp, SOAR (Summer of Open AI Research), a mentored program. [aiwiki] Copyable at zero budget: a public chat where the work happens, one concrete goal, and a mentored summer or quarterly cohort.
- BigScience: May 2021 to July 2022, "over 1000 volunteer researchers." It was organized into working groups with chairs, and "10 initial proposals grew into the set of 30 working groups." It had a collaboratively written Ethical Charter. Over 1,200 people registered. [arxiv +2] Copyable: working groups with named chairs, a charter, and a final shared paper with all participants as authors. It was not zero-budget: it had a public supercomputer compute grant. [arxiv]
- OpenHands: an academic paper with many contributors as authors (the citation lists 24 authors) gave contributors a credible, citable credit. [github]
- LAION, Nous Research, Oxen, ML Collective, Cohere Labs (Cohere For AI) community, OpenBB, Jupyter: membership ladders and governance details are unverified in this research round. I did not fetch primary governance docs for them. Do not cite them as models until you have read their docs.
- Copyable at zero budget (synthesis): (1) one named shared goal, (2) weekly public lab notes, (3) a benchmark or dataset that people can add to, (4) a paper or technical report with contributors as co-authors, (5) a visible ladder (contributor → triager → maintainer), (6) one recurring call.

### Q4. Repo mechanics ranked by effect size

| Rank | Mechanic | Evidence level | Notes |
|---|---|---|---|
| 1 | Human time-to-first-response | Strong (CHAOSS; TTFR and abandonment studies) | The single most important thing you control. |
| 2 | Mentored, well-scoped first issues | Moderate–strong (GFI mentoring study: +71% success) | Write the context into the issue. |
| 3 | accepted / issue-first gating | Practice evidence (mem0, Ghostty, Continue) | Protects your time from AI slop. Only works if humans curate it. |
| 4 | AI_POLICY.md / AGENTS.md | Practice evidence (455 rules, 102 communities) | Needed in 2026. Agents ignore it unless CI enforces it. |
| 5 | Visible ladder (maintainer nomination) | Practice (OpenHands) | Effect size unverified. |
| 6 | Release notes crediting contributors | Practice (Letta auto "New Contributors") | Cheap; effect size unverified. |
| 7 | Discord/Slack vs Discussions vs Telegram | Folklore / practice | Every case project uses Discord or Slack plus GitHub. No study ranks them (unverified). Telegram keeps you in your existing Russian-speaking circle. |
| 8 | CONTRIBUTING, issue templates, CODEOWNERS | Weak alone | You already have CONTRIBUTING, and it did not help, because the promise was not kept. |
| 9 | all-contributors bot, roadmap.md, RFCs | Folklore at your scale | RFCs only make sense once there are several regular contributors. |
| 10 | Hacktoberfest | Negative for you | The 2025 rules required 6 accepted PRs. In 2026 organizers "no longer actively incentiviz[e] PRs" because of spam. [jenkins, dev] |
| — | GSoC / Outreachy / MLH / capstones | Unverified | No retention evidence gathered this round. These need a mentoring commitment and usually an org. |
| — | GitHub Sponsors / bounties | Unverified for contributor growth | Your budget rules out bounties anyway. |

### Q5. Portfolio shape: 60 repos vs a few flagships in an org

- Mechanics (verified): a transfer moves "issues, pull requests, wiki, stars, and watchers," and keeps commit contribution history. Redirects are "permanently deleted" if you create a new repo or fork at the old location. Assignees outside the org are cleared. [github] GitHub Pages *.github.io URLs change immediately. [github]
- Org benefits (verified features): org-level PR limits (August 2026), [github] team permissions, and a neutral "lab" identity that does not read as one person's dump.
- Does an org increase outside participation? Unverified. I found no study. My recommendation rests on reasoning: 60 repos under 15 stars each split your scarce attention 60 ways. With 15 PRs across all repos, no single repo looks alive. Contributor graphs, CHAOSS Contributor Absence Factor and "recent activity" signals are per-repo, so concentrating activity makes them visible.
- Costs: a few hours of transfers, broken links in old posts (mostly covered by redirects), and package and Pages URL changes. Stars do not get lost in a transfer.

### Q6. Distribution to the right people

- Hacker News / Show HN: only for things people can run. No blog posts, lists, or newsletters. "Don't post quickly-generated one-offs." [alpstack, saascity] Do not ask friends to upvote: anti-abuse software discards ring votes, and Show HN rules say asking friends to upvote or comment is not allowed. Be present to answer comments. [launchrepo] Best fit: second-brain-starter-kit or sqlite-graph-memory with a one-command demo. Your awesome-list is not a Show HN.
- r/LocalLLaMA: about 794k subscribers; self-promotion is "Restricted," with a guideline of about 1/10 of activity and required disclosure of affiliation. [leadsrover, intoru] Write technical posts (benchmarks, failure analysis, local-model results) with the repo as context. [launchwake]
- Obsidian forum, Obsidian Discord, Lobsters, X lists, PKM newsletters: posting rules are unverified in this round. Read each forum's rules before posting. Lobsters is invite-only (from general knowledge; unverified here).
- Formats that produce contributors rather than stars (synthesis): "here is a benchmark, here is how to add your result," "here is a failing case we can't solve," and "lab notes week N." All of these invite action. "I built X" invites a star.
- Language: you can use agents to polish English. But posts must read as written by you, and readers increasingly punish undisclosed LLM text (r/LocalLLaMA removal norms cite "primarily LLM-generated content without transparency"). [intoru]

### Q7. Five early metrics, and anti-patterns

Five metrics (all CHAOSS-defined or derived):

1. Human Time to First Response (median, PRs and issues, bots excluded). Target: under 72h, then under 24h.
2. Unanswered external contributions (count with no human reply after 7 days). Target: 0.
3. Conversion rate: first-time contributors who make a second contribution within 90 days (CHAOSS "Conversion Rate" / "Newcomer Experience"). [nesbitt, chaoss]
4. Contributor Absence Factor (formerly "bus factor"): the smallest number of people who make 50% of contributions. [chaoss] Yours is 1. The first win is getting it to 2 on one flagship.
5. Change Request Closure Ratio (PRs closed or merged ÷ PRs opened per month). This shows whether you keep up. [chaoss]

Anti-patterns and how to detect them:

- Fake stars: StarScout signatures are low-activity accounts and lockstep bursts. The effect lasts under two months, then becomes a burden. [beehaw] Never buy stars. Also check that your Telegram-friend stars are not mistaken for traction.
- AI-slop PRs: require a linked accepted issue. Set a PR limit of 1–2 for non-write users, with a bypass list for proven contributors. Require a disclosure field.
- One-off awesome-list adders: they count as contributors but not as community. Track them separately and exclude them from conversion targets.
- "Help wanted" with context in your head: each issue needs the goal, the files to touch, the test command, the acceptance criteria, and "why this matters." Your agents can draft this, but you must check it.
- Bot-inflated metrics: exclude your machine account from TTFR and from contributor counts.

### Q8. The 90-day plan is in the table below.

## Comparison table of case projects

| Project | First 10 external contributors: how / when | Rituals (verified) | AI disclosure | Governance doc |
|---|---|---|---|---|
| Aider | Unverified | Benchmark results and conventions via PR; release notes | Publishes "Aider wrote X%" per release | CONTRIBUTING + individual CLA |
| OpenHands | From README-only repo (Mar 2024); early contributors met in Slack; exact timing unverified | Slack, Discord, docs, paper | Unverified | Maintainer nomination + ≥3-day discussion |
| Letta / MemGPT | Unverified | Discord, issues; auto "New Contributors" in releases | Unverified | CONTRIBUTING; PRs collaborators-only on old repo |
| Khoj | Unverified | Unverified | Unverified | Unverified |
| mem0 | Unverified | Issue-first, accepted label, PR Gate, Discussions, vouch list | Required; "an agent wrote this, here is what I verified" welcome | CONTRIBUTING, AGENTS.md, Code of Conduct, CLA |
| SillyTavern | Unverified | Templates; ~200-line soft PR limit | "We do not prohibit nor encourage" AI; you are responsible | CONTRIBUTING |
| Cline | Hackathon project; community grew via MCP servers, rules, guides; timing unverified [cline] | Discord #contributors, r/cline, $1M grant program | Unverified | CONTRIBUTING |
| Continue | Unverified | Project board of ideas, Discussions, issue-first, screen recording for features | None seen | CONTRIBUTING + CLA; README suggests a possible sunset (unverified) |
| crewAI | Unverified | Unverified | Unverified | Unverified |
| smolagents | Unverified | Contribution guide | Unverified | CONTRIBUTING (not read) |
| Dataview / Smart Connections | Unverified | Unverified | Unverified | Unverified |
| Copilot for Obsidian | Unverified | Discord for dev, Discussions | Unverified; AGENTS.md exists | CONTRIBUTING; paid Plus tier |
| Ghostty (reference) | Unverified | Vouch requests in Discussions [codenote] | Required since Aug 2025; AI only for accepted issues since Jan 2026 [redmonk] | AI_POLICY.md |
| EleutherAI (lab) | Discord founded July 2020 around the GPT-3 replication goal | Public Discord, SOAR mentorship | n/a | Non-profit since early 2023 |
| BigScience (lab) | Launch event with 10 working-group proposals → 30 groups [openreview] | Working groups with chairs [arxiv] | n/a | Ethical Charter; RAIL license [arxiv, arxiv] |

## The 90-day plan (start: week of October 12, 2026)

| # | Action (in order) | Maintainer hrs/week | Expected effect | Day 30 | Day 60 | Day 90 |
|---|---|---|---|---|---|---|
| 1 | Clear the backlog personally. Reply to all 7 ignored PRs and every open external item: apologize, then merge, request changes, or close with thanks and a reason. | 4h in week 1, then 0 | Repairs trust with the 3+ people who already tried. Highest-probability returners. | 0 items without a human reply | ≥1 of the original external contributors makes a new contribution | ≥2 returners |
| 2 | Split identities. Create one machine account or GitHub App for the agent fleet. Agents stop posting as @tonydzi. Add a one-line disclosure header to agent posts. | 3h once, then 0.5h | Strangers know when a human is speaking. Complies with the spirit of the ToS. | 100% of agent posts come from the bot identity | Bot excluded from metrics | Same |
| 3 | Replace the 48h promise with a kept 72h human-response SLA, weekdays only, on flagship repos only. Daily 20-minute triage slot. | 2–3h | Lowers TTFR, which is the strongest lever in the evidence. | Median human TTFR < 72h | < 48h | < 24h on flagships |
| 4 | Pick 2–3 flagships (suggested: sqlite-graph-memory, second-brain-starter-kit, verbatim-citation-gate) and transfer them to an org. Archive or label the rest as "lab notebook – not seeking contributions." | 4h once, then 0 | Concentrates attention and activity signals. Enables org-level PR limits. | Org live; READMEs updated; redirects tested | Contributor graph shows ≥2 humans on one flagship | Contributor Absence Factor = 2 on one flagship |
| 5 | Write 5 "context-complete" accepted issues per flagship (goal, files, test command, acceptance criteria, rough size). Agents draft; you edit. | 2h | Makes good first issues finishable without your head. | 15 such issues open | ≥3 taken by strangers | ≥5 merged from strangers |
| 6 | Publish AI_POLICY.md + AGENTS.md (disclosure required, human must be able to explain the change, accepted issue first). Set a PR limit of 2 for non-write users with a bypass list. Add an Aider-style line to releases: "Agents wrote X% of this release; reviewed by a human." | 3h once | Turns your agent fleet into a credible, disclosed method. Screens out slop. | Policy merged on all flagships | First bypass-list member | Policy cited or used by ≥1 contributor's PR |
| 7 | Build one public lab artifact: an open benchmark for second-brain / agent-memory retrieval (e.g., verbatim-citation accuracy on Obsidian-style vaults), where people contribute results and test cases via PR, like Aider's leaderboard. | 3h | Gives outsiders a reason to join "a lab," and gives hiring engineers something rigorous to judge. | v0 spec + 1 baseline published | ≥3 external result or test-case PRs | Short technical report with contributors credited as co-authors |
| 8 | Weekly lab notes (one short post, written by you, agent-polished English, disclosed) + one monthly 45-minute public lab call (Discord or Meet). Move community chat from Telegram to an English Discord or GitHub Discussions. | 2h | A ritual that makes "the lab" visible. Builds a returning audience. | 4 notes; 1 call held | ≥5 non-acquaintance attendees or commenters | ≥3 regulars |
| 9 | One distribution push per month, technical and tryable: a Show HN for the flagship with a one-command demo; a benchmark write-up on r/LocalLLaMA (follow the ~1/10 rule, disclose affiliation); an Obsidian forum post (read its rules first). No vote solicitation. | 2h | Reaches builders, not friends. Each post links to the benchmark's "add your result" page. | 1 post | 2 posts; ≥1 contributor from a post | ≥3 contributors whose first touch was a post |
| 10 | Publish a ladder (GOVERNANCE.md): contributor → triager (bypass list, triage role) → co-maintainer (nomination plus a discussion period, OpenHands-style). Credit contributors in every release. | 1h | Gives returners a next step. Reduces Contributor Absence Factor. | Doc published | First triager named | First co-maintainer nominated on one flagship |

Total load: about 8–10 hours a week after week 1. If you have less time, drop #9 before dropping #1–#3.

STOP doing:

- Letting agents reply to humans under your personal account, and letting agents give the first reply to any newcomer.
- Promising "48h" anywhere you do not actually meet it.
- Creating new public repos. Every new repo divides your attention further.
- Labeling issues good first issue / help wanted when the context lives only in your head.
- Counting Telegram-acquaintance stars, clones, or awesome-list adds as community traction.
- Opting into Hacktoberfest or similar quota-driven events.
- Letting your fleet open PRs to other projects without first checking and enforcing their AI policy. Agents will not do this themselves, and a ban there would hurt your hiring goal.

## What would make this fail

- You stay the bottleneck. If the daily triage slot slips, TTFR goes back to days and everything else is wasted. This is the most likely way to fail.
- Agents keep impersonating you. One discovered case of an agent arguing with a human as "you" can destroy trust. That trust is exactly what frontier-lab hiring engineers check.
- The lab artifact is not rigorous. A benchmark that is easy to game, or written as marketing, will be ignored or criticized on HN and r/LocalLLaMA. Publish methods, limitations and negative results.
- Spreading across 60 repos again. Contributors cannot find "the project" if there are sixty of them.
- AI-slop inflow overwhelms you after a successful post. Without PR limits, accepted-issue gating and a disclosure rule set up in advance, one viral post can create weeks of review debt. tldraw's response was to close all external PRs. [pickuma]
- Platform risk. GitHub's bot-account enforcement is opaque (one reported month-long hiding of a disclosed bot). [dev] Keep the machine account low-volume and clearly human-owned.
- Language and tone. Over-polished, obviously generated English in community posts reads as slop. Short, honest, slightly imperfect English written by you is better.

## Caveats

- Search budget ran out before I could gather primary sources for Khoj, crewAI, Dataview, Smart Connections, LAION, Nous Research, Oxen, ML Collective, Cohere Labs, OpenBB, Jupyter, GSoC/Outreachy outcomes, and Obsidian forum or Lobsters rules. Everything about them above is marked unverified.
- No source gave "first 10 contributors" timing or median response times for any case project. Those cells are unverified, not estimates.
- Some details (Ghostty's April 2026 move off GitHub, the 50% disclosure rate, the Kubernetes/Rust trailer bans, the Hacktoberfest 2026 FAQ quote, Octoverse first-time-contributor records) come from secondary write-ups, not the primary pages.
- The org-move and lab-artifact recommendations rest on reasoning from verified mechanics and case patterns. No causal study supports them.

## Sources (64 unique URLs extracted from the artifact's citation chips)

https://visualstudiomagazine.com/articles/2026/06/30/github-extends-contribution-controls-from-prs-to-issues.aspx
https://github.blog/open-source/maintainers/how-pull-request-limits-are-cutting-down-the-noise/
https://github.blog/changelog/2026-08-06-set-pull-request-limits-at-the-organization-level/
https://github.com/mem0ai/mem0/blob/main/CONTRIBUTING.md
https://x.com/mitchellh/status/2014433315261124760?lang=en
https://www.chaoss.community/kb/metrics-model-starter-project-health/
https://nesbitt.io/2026/05/27/chaoss-metrics-in-2026.html
https://blog.adafruit.com/2026/02/20/the-open-source-world-can-write-its-own-rules-for-ai-and-nobody-has-to-ask-permission/
https://github.com/Aider-AI/aider/blob/4bf56b77/aider/website/HISTORY.md
https://eleuther.ai/about/
https://openreview.net/pdf?id=2e346l2PPOm
https://arxiv.org/pdf/2211.05100
https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository
https://favors.dev/blog/show-hn-launch-guide
https://saascity.io/blog/how-to-launch-an-ai-product
https://intoru.ai/subreddits/localllama
https://dev.to/_firelinks/hacktoberfest-2026-stopped-counting-prs-how-id-spend-the-month-instead-48d5
https://www.chaoss.community/kb/metric-time-to-first-response/
https://zenodo.org/records/7747317
https://www.researchgate.net/publication/id_503f9e0f_Understanding_the_Time_to_First_Response_In_GitHub_Pull_Requests
https://whystar.github.io/res/paper/abPR_TSE2021.pdf
https://www.openhands.dev/blog/openhands-from-readme-to-open-source-movement
https://openreview.net/pdf/id_94b58ea4cff8b93c33af989ecf4ac58bde9bb.pdf
https://docs.openhands.dev/overview/contributing
https://cline.bot/blog/cline-the-fastest-growing-ai-open-source-project-on-github-in-2025-thanks-to-you
https://github.com/cline/cline
https://cline.ghost.io/5m-installs-1m-open-source-grant-program/
https://github.com/Aider-AI/conventions
https://aider.chat/docs/leaderboards/contrib.html
https://github.com/Aider-AI/aider/blob/main/CONTRIBUTING.md
https://github.com/continuedev/continue/blob/main/CONTRIBUTING.md
https://github.com/continuedev/continue
https://github.com/SillyTavern/SillyTavern/blob/release/CONTRIBUTING.md
https://github.com/SillyTavern/SillyTavern
https://github.com/letta-ai/letta
https://github.com/letta-ai/letta/releases
https://github.com/logancyang/obsidian-copilot/blob/master/CONTRIBUTING.md
https://x.com/paulgauthier/status/1928594477083410702
https://redmonk.com/kholterhoff/2026/02/03/ai-slopageddon-and-the-oss-maintainers/
https://withstoa.com/blog/mitchell-hashimoto-on-the-ai-assisted
https://newsletter.specstory.com/p/mitchell-hashimoto-on-the-ai-assisted
https://codenote.net/en/posts/oss-ai-slop-contribution-policy-shift/
https://itsfoss.com/news/mitchell-hashimoto-vouch/
https://dev.to/nefayran/what-30-open-source-projects-ask-of-ai-assisted-contributions-4il0
https://www.generativelabs.com/insights/open-source-ai-contribution-rules
https://pickuma.com/for-dev/open-source-maintainers-rejecting-ai-pull-requests/
https://docs.github.com/en/site-policy/github-terms/github-terms-of-service
https://github.com/navikt/copilot/issues/1508
https://dev.to/talon_agent/github-hid-my-account-for-a-month-no-notice-no-reason-no-human-h1c
https://aiwiki.ai/wiki/eleutherai
https://arxiv.org/pdf/2305.18615
https://github.com/AI-App/All-Hands-AI.OpenHands
https://www.jenkins.io/blog/2025/09/24/hacktoberfest-2025-intro/
https://docs.github.com/en/enterprise-server@3.13/repositories/creating-and-managing-repositories/transferring-a-repository
https://github.com/orgs/community/discussions/188227
https://alpstack.com/product-launch-sites/hacker-news-show-hn
https://launchrepo.dev/directories/hackernews/
https://leadsrover.io/blog/reddit-self-promotion-rules-by-subreddit
https://www.launchwake.com/channels/r-localllama
https://www.chaoss.community/kb/metric-newcomer-experience/
https://www.chaoss.community/kb/metric-contributor-absence-factor/
https://www.chaoss.community/practitioner-guide-responsiveness/
https://beehaw.org/post/17683690
https://arxiv.org/pdf/2509.25397


===== VENDOR: glm (glm.md) =====
---
dr: DR26-10-08-ZB-01-1645
rail: glm#web
account: chat.z.ai, profile "PaloAlto Ai Research Lab"
mode: GLM-5.2 + Deep Think Max + web search ON (globe toggle, "Searching the web" observed)
chat: https://chat.z.ai/c/s_3cea3877
sent: 2026-10-08 16:53 PDT
collected: 2026-10-08 17:04 PDT
collected_by: Claude Code (Fable 5.1) on NODE-0X-2023PAL via local Chrome get_page_text
quality_note: citation chips present (opensourcealternatives, eleuther, mlcollective, allcontributors, reddit, mintlify, skillselion, medium, github) but URLs not rendered in page text; several effect sizes ("300%+", "40% higher return", "5x engagement", "<24h") carry no primary source and are treated as low-authority. Per-project "first 10 contributors / TTFR" cells look inferred, not sourced.
Machine: NODE-0X-2023PAL · Agent: Claude Code · Operator: dev · 2026-10-08
---

# Deep Research: From Solo Agent Lab to Contributor Community (GLM-5.2)

## Executive Summary
- The contributor funnel in agent/LLM OSS is broken: even popular tools like OpenHands (74k+ stars) and Aider (44k+ stars) report contributor-to-star ratios below 0.1%, with most contributions coming from a small inner circle [opensourcealternatives +1]. Your 15 PRs across 60 repos is actually above average for projects under 15 stars.
- Time-to-first-response is the critical bottleneck: CHAOSS metrics show that response times under 48 hours dramatically improve newcomer retention. Your current 4-day average (and 47% no-reply rate) is actively repelling potential contributors.
- "Lab as community" framing works at zero budget: EleutherAI grew from 0 to 15+ staff and dozens of volunteers by treating their GitHub org as a public research notebook, not a product [eleuther +1]. Their model is copyable.
- AI-authored contributions need transparent labeling: No major project has solved this yet. The "opensource-guide-coach" skill [skillselion] represents the state of the art in agent-assisted maintainer coaching, not contributor interaction.
- Fragmentation is killing your contribution flow: 60 small repos create cognitive overhead for outsiders. Evidence from monorepo discussions [mintlify +1] suggests 3-5 flagship repos under one org would increase participation.
- Obsidian/second-brain communities are concentrated on Discord and Reddit: r/ObsidianMD, r/AI_Agents, and specialized Discords (e.g., notebooklm-alternative topic) [github] are where your audience lives. HN and Lobsters have lower conversion for PKM tools.
- Good-first-issue hygiene has the highest evidence-based impact: CHAOSS practitioner guides show that well-scoped first issues improve retention by 300%+ compared to "help wanted" labels alone. (low-authority: no primary URL)
- All-contributors bot provides measurable recognition ROI: projects using it show 40% higher contributor return rates [allcontributors +1]. It costs zero hours once installed. (low-authority)
- Hacktoberfest 2025-2026 has become a liability: AI-slop PRs now constitute 40%+ of October contributions to popular repos [reddit +1]. You should explicitly opt out or implement spam filters.
- The frontier lab hiring pathway runs through visible research artifacts: hiring engineers evaluate candidates' ability to build credible communities around their research, not just code quality (unverified, based on general hiring trends).

## Per-Question Findings

### 1. What converts strangers into first-time contributors
| Project | First 10 external contributors | Time-to-first-reply | Rituals | Bounties |
|---|---|---|---|---|
| OpenHands | From early Discord community, many became contributors after using the tool for work projects [opensourcealternatives] | <24h on Discord, <48h on GitHub | Weekly "Office Hours" on Discord, RFC process on GitHub Discussions, public roadmap | No |
| Aider | Terminal-first developers from HackerNews and r/programming [opensourcealternatives] | <12h (maintainer is active) | Git-native workflow (commits visible), changelog with contributor credits | No |
| Cline | VS Code extension users, many from Cursor migration [opensourcealternatives] | <36h on GitHub | Discord for support, GitHub for feature requests, "Plan/Act" permission model | No |
| Continue | JetBrains users specifically, as VS Code was overserved [opensourcealternatives] | <48h | Model flexibility as selling point, contributor docs in JetBrains format | No |
| EleutherAI | Researchers wanting open models, many from academic institutions [eleuther +1] | <24h on Discord | Weekly research calls, public paper drafts, "open science" framing | No (non-profit) |
| ML Collective | "Genuinely curious" self-learners, many career switchers [mlcollective +1] | <24h | Open Collab meetings, mentorship pairing, research training groups | No |

Key conversion factors: tool utility first (contributors come from users who need the tool for their own work); Discord > GitHub Discussions (real-time chat shows 5x higher engagement for agent projects [medium], low-authority); visible maintainer activity (daily commits and quick replies signal project health); clear contribution ladder ("good first issue" → "help wanted" → "maintainer" paths retain 3x more contributors, low-authority).

Your gap: your 4-day response time and 47% no-reply rate are below the threshold where contributors abandon projects. The 48h promise in CONTRIBUTING.md is being violated.

### 2. Solo maintainer + AI agents: disclosure and trust
- No major project has formal AI authorship policies (GLM claim; contradicted by claudeai leg: mem0, Ghostty, TypeScript, Linux kernel have them).
- Some projects tag agent-authored commits with [agent] prefixes (unverified).
- AI-slop PRs are now a recognized problem, with 40%+ of Hacktoberfest contributions being low-quality AI-generated [reddit +1].
- Recommendation: implement a 🤖 agent-authored label for issues/PRs generated by your coding agents. Disclosure helps rather than hurts trust; contributors appreciate knowing what they're engaging with.

### 3. "The lab is the community": zero-budget models
| Collective | Membership ladder | Governance docs | Public artifacts | Budget model |
|---|---|---|---|---|
| EleutherAI | Volunteer → Contributor → Researcher → Staff [eleuther +1] | Public charter, contributor covenant | Weekly research notes, model cards, paper drafts | Non-profit, grants |
| ML Collective | Member → Mentor → Research lead [mlcollective +1] | Open Collab framework, mentorship guide | Training curricula, research benchmarks | Volunteer-run |
| Nous Research | (not in search results, unverified) | | | |

Zero-budget copyable elements: public research notebook (turn clawrush into weekly "Lab Notes" on the site); open roadmap with contributor slots (GitHub Projects with "Help Wanted" columns); weekly Discord office hours; contributor recognition ladder ("Contributor" → "Core Contributor" → "Research Collaborator" in README); public paper drafts.

### 4. Repo-level mechanics ranked by effect size
- Time-to-first-response: <48h improves retention by 300%+ (low-authority).
- Good first issues: properly scoped issues increase completion rate from 15% to 60% (low-authority).
- All-contributors bot: 40% higher return rates [allcontributors +1] (low-authority).
- Office hours: low evidence but high anecdotal support in agent communities [medium].
- Hacktoberfest: now net-negative due to AI-slop PRs [reddit +1].
- CODEOWNERS: low evidence for solo maintainer projects.
- University partnerships: no evidence in search results (unverified).

### 5. Portfolio shape: 60 small repos vs monorepo
Monorepo discussions [mintlify +1] highlight maintenance trade-offs but don't address contributor experience. Agent projects with multiple repos (like OpenHands) use GitHub orgs effectively. 60 repos create decision paralysis.

Recommendation: create a GitHub organization "palo-alto-ai-lab" with 3-5 flagship repos: second-brain-kit (merge sqlite-graph-memory + second-brain-starter-kit); agent-canon (merge claude-bible + verbatim-citation-gate); agent-connectors (merge telegram-mcp-kit + whatsapp-mcp-kit); lab-notes (the build diary); awesome-verified-agents (keep as curated list). Costs: redirect rot (GitHub handles this automatically), lost stars (minimal), gains in discoverability and onboarding.

### 6. Distribution channels
| Channel | Activity | Contributor conversion | Rules to avoid bans |
|---|---|---|---|
| r/ObsidianMD | High | Medium (PKM focused) | No self-promotion in titles, contribute to discussions first |
| r/AI_Agents | High | High (agent builders) | Follow 9:1 rule, use "Share" not "Promote" |
| r/LocalLLaMA | Medium | Medium (self-hosting) | Technical depth required, no "look what I built" posts |
| Obsidian Discord | High | Low (plugin focused) | No bot commands in #general, use #showcase |
| NotebookLM Alternative Discord [github] | Medium | High (PKM+agents) | Active participation required |
| HN | Low for PKM | Low | Submit to "Show HN" with technical depth |
| Lobsters | Low | Low | Invite-only, technical focus |

Posting formats that produce contributors: "I built X to solve Y problem, here's the technical approach, what would you do differently?"; "Weekly lab notes: progress on Z, stuck on W, here's the code"; "Open challenge: can anyone improve this benchmark by 10%?"

### 7. Metrics and anti-patterns
Five metrics: TTFR (<48h target); newcomer retention at 90 days; issue-close ratio (healthy 70-80%); bus factor (currently 1, target 3 within 6 months); contributor diversity ratio (% not from immediate network).

Anti-patterns: fake stars (sudden spikes from accounts with no activity [reddit]); AI-slop PRs during Hacktoberfest [opensource +1]; awesome-list adders who never return [github]; context-hidden issues that reference internal agent conversations.

### 8. 90-Day Plan
| Day | Action | Hrs/week | Expected effect | Checkpoint |
|---|---|---|---|---|
| 0-30 | Consolidate portfolio: create palo-alto-ai-lab org, merge 60→5 repos | 8h | Reduced cognitive load, clearer entry points | 5 repos live, redirects working |
| 0-30 | Implement response SLA: 48h reply guarantee, use agents for triage | 5h | Stop losing potential contributors | TTFR <48h for all open issues |
| 0-30 | Install all-contributors bot | 2h | Immediate recognition | Bot running, first contributors added |
| 30-60 | Launch "Lab Notes": weekly public build diary on site | 4h | "Lab" narrative, research credibility | 4 weekly notes published |
| 30-60 | Start Discord office hours: weekly 1h | 1h | Real-time community building | 3+ regular attendees |
| 30-60 | Good-first-issue audit: 10 properly scoped issues | 6h | Clear entry points | 10 issues with clear scope |
| 60-90 | Agent disclosure framework: label agent-authored content | 3h | Trust through transparency | All agent PRs labeled |
| 60-90 | Targeted distribution: bi-weekly posts in r/AI_Agents, Obsidian Discord | 3h | Reach right audience | 2 posts per channel, 5+ referrals |
| 60-90 | Contributor ladder: "Contributor → Core → Researcher" | 2h | Clear progression | Ladder published, 2 contributors promoted |
| Ongoing | STOP: maintaining 60 repos, responding after 4 days, ignoring PRs | -8h | Free up time | |

STOP immediately: maintaining 60 separate repos; letting PRs sit >48h; treating all repos equally; posting to HN/Lobsters (low ROI for PKM, GLM's claim, contradicted by claudeai leg); accepting all awesome-list PRs (curate instead).

## Comparison table
| Project | First 10: how | When | Rituals | AI disclosure | Governance doc |
|---|---|---|---|---|---|
| OpenHands | Discord users needing autonomous agents | 2023-2024 | Office hours, RFCs | None | CONTRIBUTING.md, roadmap |
| Aider | HN/Reddit terminal enthusiasts | 2023 | Git-native workflow | None (contradicted by claudeai leg: "Aider wrote X%" per release) | README, contributor guide |
| Cline | Cursor/VS Code migrants | 2024 | Discord support | None | Extension docs |
| Continue | JetBrains users | 2024 | Model flexibility docs | None | Configuration docs |
| EleutherAI | Academic researchers | 2020 | Weekly calls, paper drafts | None | Non-profit charter |
| ML Collective | Self-learners, career switchers | 2021 | Open Collab, mentorship | None | Community framework |
| Your portfolio | Russian-speaking acquaintances | 2024-2026 | None | None | CONTRIBUTING.md (48h promise, unfulfilled) |

## What would make this fail
- AI-slop takeover: without filters, Hacktoberfest 2026 could bring 100+ low-quality PRs.
- Disclosure backlash: human contributors may feel deceived when they discover "the maintainer" is actually 8 machines.
- Org migration rot: redirects misconfigured → lose PRs/followers.
- Office hours emptiness: weekly sessions nobody attends signal rejection.
- Frontier lab disinterest: "lab" framing that appears performative reads as gimmicky.
- TTFR regression after initial improvement.
- Good-first-issue context collapse: issues requiring knowledge only in your head stay unfinished.

Success requires: ruthless focus on 3 repos, 48h response SLA, transparent agent labeling, consistent "lab notes" publishing. Community building in agent/LLM OSS is fundamentally about trust through transparency and responsiveness, not just technical quality.

## Sources (35 URLs pulled from the z.ai "Sources" panel of the chat; GLM's own search hits, many only tangential)
https://www.inclusion-ai.org/blog/agentic-ai-202606
https://www.opensourcealternatives.to/blog/best-open-source-ai-coding-assistants
https://www.kunalganglani.com/blog/claude-code-alternatives-open-source
https://github.com/ai-boost/awesome-harness-engineering
https://o-mega.ai/articles/top-10-open-source-ai-coders-2026
https://arxiv.org/html/2608.05201v1
https://www.techtarget.com/it-infrastructure/tip/Vibe-coding-is-killing-open-source-increasing-software-risk
https://skillselion.com/skills/xixu-me/skills/opensource-guide-coach
https://github.com/FlorianBruniaux/claude-code-ultimate-guide/blob/main/IDEAS.md
https://www.researchgate.net/publication/id_30860f0f_The_Rise_of_Autonomous_AI_Agents_A_Comprehensive_Survey_of_OpenClaw_-Architecture_Security_Ecosystem_and_Beyond
https://eleuther.ai/community
https://www.eleuther.ai/
https://eleuther.ai/about
https://mlcollective.org/community
https://mlcollective.org/
https://www.reddit.com/r/hermesagent/comments/1wlkfiv/frustrated
https://www.reddit.com/r/AI_Agents/comments/1tjtqm5/karpathys_llmwiki_for_agentic_software_development
https://github.com/topics/notebooklm-alternative
https://www.reddit.com/r/getrecall/comments/1sz2tdq/andrej_Teague_just_described_recall_without
https://medium.com/@techlatest.net/ai-agent-arsenal-20-battle-tested-open-source-powerhouses-ea3d4534d264
https://www.mintlify.com/blog/when-do-you-really-need-a-monorepo
https://gitdoc.ai/resources/github-examples
https://www.m365.fm/guests/mirko-peters
https://moxiedocs.com/blog/agents-md-explained-how-to-write-one
https://github.com/github/spec-kit/discussions/152
https://www.reddit.com/r/programming/comments/1m0qxf4/death_by_a_thousand_slops
https://dev.to/elshadhu/i-built-a-tool-to-stop-wasting-time-on-toxic-open-source-projects-5h12
https://news.ycombinator.com/item?id=46717556
https://opensource.org/wp-content/uploads/2025/10/osi_maintainers.pdf
https://github.com/topics/spam-filtering
https://allcontributors.org/en/bot
https://github.com/all-contributors/app
https://allcontributors.org/en/bot/usage
https://handbook.gitlab.com/handbook/people-group/general-onboarding
https://dev.to/opensauced/how-to-create-a-welcoming-space-for-new-open-source-contributors-25fd

---

**Claude:**

{"lang":"mixed","topic":"Как превратить соло-портфель репо tonydzi в комьюнити контрибьюторов лаборатории Palo Alto AI","one_line":"Какие механики привлечения контрибьюторов работают для соло-мейнтейнера с агентным флотом (кейсы Aider/OpenHands/Cline/mem0/EleutherAI) и каков 90-дневный план для tonydzi / Palo Alto AI Research Lab.","key_findings":["Главная проблема — не видимость, а отзывчивость и доверие: 7 из 15 внешних PR остались без человеческого ответа (47%), первые ответы идут ~4 дня при обещанных в CONTRIBUTING 48 ч; обе ноги сходятся, что TTFR — главный рычаг (CHAOSS; исследования TTFR и PR-abandonment). Обещание, которое не выполняется, хуже отсутствия обещания.","Агенты пишут под личным аккаунтом @tonydzi, и посторонние не отличают человека от машины. По ToS GitHub владелец отвечает за всё под аккаунтом, допускается один бесплатный machine account; claudeai-нога рекомендует отдельный бот-аккаунт/GitHub App и строку-раскрытие в каждом агентном посте.","Раскрытие ИИ-авторства стало нормой, а не исключением: 455 правил из 102 сообществ (Yang/He/Zhou, arXiv июль 2026); Aider публикует «Aider wrote 79% of the code in this release» (70–80% по релизам) и растёт; mem0 автозакрывает PR без accepted-issue и ведёт vouch-список; Ghostty с янв. 2026 принимает AI-PR только по accepted issues; Linux kernel требует тег Assisted-by. Утверждение GLM-ноги «формальных политик нет» опровергнуто.","Good-first-issue слабеет: по 406 826 issue и 1 117 PR (EASE 2026) вовлечённость новичков стабильна ~27%, доля GFI упала с ~0.9% до 0.6%, merge-rate новичковых GFI-PR упал с 61.9% до 42.2%; менторство даёт +71% успеха первого вклада (Tan et al., ICSE 2023). Метка без человеческого ревью не конвертирует.","GitHub в 2026 добавил рычаги против слопа: отключение PR (фев.), лимит открытых PR для пользователей без write-доступа с bypass-списком (17 июня), настройка на уровне организации (6 авг.), ограничение создания issue. PR от Copilot/агентов в лимит засчитываются.","«Лаба = комьюнити» формируется вокруг одного артефакта и публичного места работы: EleutherAI (Discord июль 2020, цель — воспроизвести GPT-3, нет жёсткой границы сотрудник/волонтёр, SOAR-менторство), BigScience (1000+ исследователей, 10 предложений → 30 рабочих групп, этическая хартия), OpenHands (README-only в марте 2024 → 188+ контрибьюторов к статье ICLR 2025, лестница мейнтейнера с обсуждением ≥3 дней), Cline (хакатон → «самый быстрорастущий AI OSS» по Octoverse 2025, грант $1M).","Фрагментация вредит: 60 репо с <15 звёзд дробят внимание. Перенос репо в организацию сохраняет звёзды, issues, PR, watchers и редиректы (ломаются при создании нового репо на старом пути; Pages-URL меняются). Исследований, что организация повышает участие, не найдено — рекомендация на рассуждении. Обе ноги сходятся на 2–5 флагманах (claudeai: sqlite-graph-memory, second-brain-starter-kit, verbatim-citation-gate; GLM: слияние в 3–5 репо).","Дистрибуция должна быть «пробуемой»: Show HN требует запускаемого продукта (не блог/список), просьбы об апвоутах запрещены; r/LocalLLaMA ~794k, самопромо ≈1/10 активности с раскрытием аффилиации; Hacktoberfest 2026 отказался от квоты PR из-за спама — не канал контрибьюторов. GLM-утверждение «HN/Lobsters не нужны» противоречит claudeai (Show HN подходит для second-brain-starter-kit с демо одной командой).","Накрутка звёзд — ловушка: StarScout нашёл 4.5 млн подозрительных звёзд (после фильтра 3.1 млн от 278 тыс. аккаунтов в 15 835 репо); эффект <2 месяцев, потом обуза. Метрики: человеческий TTFR (бот исключить), число внешних вкладов без ответа >7 дней (цель 0), конверсия во второй вклад за 90 дней, Contributor Absence Factor (сейчас 1, цель 2), Change Request Closure Ratio.","Качество источников неравное: у GLM-ноги числа вроде «300%+», «+40% return», «5x engagement» без первоисточников, а ячейки «первые 10 контрибьюторов/TTFR» по проектам выглядят выведенными; у claudeai-ноги Khoj, crewAI, Dataview, Smart Connections, LAION, Nous, Oxen, ML Collective, Cohere Labs, OpenBB, Jupyter, GSoC/Outreachy честно помечены unverified."],"recommendations":["Неделя 1: лично ответить на все 7 проигнорированных PR и все открытые внешние обращения (извиниться, смержить/запросить правки/закрыть с причиной) — это самые вероятные «возвращенцы».","Разделить идентичности: один machine account или GitHub App для флота агентов, агенты не постят как @tonydzi; в каждом агентном посте строка «Drafted by an agent (model X); reviewed by @tonydzi»; первый ответ новичку — всегда человек; использовать трейлер Assisted-by, избегать AI Co-authored-by.","Заменить обещание 48 ч на выполнимое: 72 ч SLA в будни только на флагманах, ежедневный 20-минутный слот триажа; цели медианы TTFR <72 ч к дню 30, <48 к 60, <24 к 90.","Выбрать 2–3 флагмана, перенести в организацию, остальное архивировать/пометить «lab notebook – not seeking contributions»; новых публичных репо не создавать.","Написать по 5 «контекстно-полных» accepted-issue на флагман (цель, файлы, команда теста, критерии приёмки, размер) — агенты черновят, человек правит; цель — 15 открытых, ≥3 взяты посторонними к дню 60, ≥5 смержено к дню 90.","Опубликовать AI_POLICY.md + AGENTS.md (раскрытие обязательно, accepted issue сначала), лимит 2 PR для пользователей без write-доступа с bypass-списком, строку в релизах в стиле Aider «агенты написали X%; проверено человеком».","Собрать один публичный лабораторный артефакт — открытый бенчмарк для second-brain/agent-memory retrieval (например точность дословных цитат на Obsidian-подобных волтах) с вкладом результатов через PR как лидерборд Aider; к дню 90 — технический отчёт с контрибьюторами как соавторами.","Ритуалы: еженедельные lab notes (пишет сам, раскрытие), ежемесячный публичный 45-минутный созвон, перенос чата с Telegram в англоязычный Discord/GitHub Discussions; опубликовать GOVERNANCE.md с лестницей contributor → triager → co-maintainer.","Дистрибуция раз в месяц и только технически: Show HN с демо одной командой, бенчмарк-пост на r/LocalLLaMA, пост на форуме Obsidian (сначала прочитать правила); без просьб о голосах. Не участвовать в Hacktoberfest; не позволять флоту открывать PR в чужие репо без проверки их AI-политики. Нагрузка ~8–10 ч/нед; при нехватке времени отсекать пункт дистрибуции раньше пунктов 1–3."],"entities":{"people":["Paul Gauthier","Mitchell Hashimoto","Robert Brennan","Graham Neubig","Connor Leahy","Sid Black","Leo Gao","Tan et al. (ICSE 2023)","Hoshikawa, Tanaka, Shimari, Kula, Matsumoto (EASE 2026)","Wenhao Yang, Runzhi He, Minghui Zhou","He, Yang, Burckhardt, Kapravelos, Vasilescu, Kästner (StarScout)"],"companies":["GitHub","EleutherAI","BigScience","CHAOSS","ML Collective","Cohere Labs","Nous Research","LAION","Palo Alto AI Research Lab","Anthropic (claude.ai)","Z.ai (GLM)"],"products_tools":["Aider","OpenHands","Letta/MemGPT","Khoj","mem0","Cline","Continue","SillyTavern","crewAI","smolagents","Ghostty","Vouch","Copilot for Obsidian","Dataview","Smart Connections","all-contributors bot","GitHub PR limits","Hacktoberfest","Show HN","r/LocalLLaMA","Discord","sqlite-graph-memory","second-brain-starter-kit","verbatim-citation-gate","AI_POLICY.md","AGENTS.md","GOVERNANCE.md","CHAOSS Time to First Response"]},"open_questions":["Как именно каждый кейс-проект получил первых 10 внешних контрибьюторов и какова их медианная скорость первого ответа — первоисточников нет ни у одной ноги.","Повышает ли перенос в организацию внешнее участие — исследований не найдено, рекомендация держится на рассуждении.","Не изучены первичные источники по Khoj, crewAI, Dataview, Smart Connections, LAION, Nous Research, Oxen, ML Collective, Cohere Labs, OpenBB, Jupyter, GSoC/Outreachy/MLH; правила Obsidian-форума и Lobsters не проверены.","Вторичные данные требуют проверки по первоисточникам: уход Ghostty с GitHub в апреле 2026, ~50% PR с раскрытием ИИ, запреты AI-трейлеров в Kubernetes/Rust/Node.js, цитата FAQ Hacktoberfest 2026.","Привёл ли публичный процент «Aider wrote X%» к росту числа контрибьюторов — причинность не доказана.","Статус Continue (README в прошедшем времени — возможный sunset) и устойчивость machine-аккаунтов на GitHub (единичный случай скрытия бота на месяц) не подтверждены.","Реальный состав и названия 60 репо и текущие метрики tonydzi — аудит репо ещё предстоит; шесть ног из шести в реестре: на диске получены только 2 (claudeai и glm)."],"related_concepts":["Time to First Response (CHAOSS)","раскрытие ИИ-авторства / AI policy","разделение идентичности человека и агента","Contributor Absence Factor / bus factor","good first issue и менторство","accepted-issue gating и лимиты PR","лаборатория как комьюнити / открытый бенчмарк","консолидация портфеля в организацию","дистрибуция Show HN / r/LocalLLaMA","фейковые звёзды (StarScout)","90-дневный план контрибьюторов","GitHub-коммуникация tonydzi (§4.7)"]}
