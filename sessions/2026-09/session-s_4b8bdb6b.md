---
session: s_4b8bdb6b
date: 2026-09-22
words: 8983
turns: 3
tools: "Bash"
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-09-22 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_4b8bdb6b` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-09-14-ZB-09-2008
REGISTRY TOPIC: Форензика доходов frontier LLM-лабораторий: сходится ли подписочная и enterprise арифметика (OpenAI, Anthropic, xAI, Mistral, Perplexity, Cohere) (через dr_start; ПОТРЕБИТЕЛЬ: оператор — внутренняя документация лаборатории: устойчивость рынка LLM-лабораторий перед рейзом/acqui-hire (две витрины)) (dr_reconcile 2026-09-21: на диске 3/6 ног, в реестре стояло 'running' — статус выправлен по факту. Тело ног: D:\Vault\Vault-Knowledge\_machine-bus\_dr\queue\DR26-09-14-ZB-09-2008\results)

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


===== VENDOR: report (DR26-09-14-ZB-09-2008.md) =====
---
id: DR26-09-14-ZB-09-2008
date: 2026-09-14 20:08:24
theme: Форензика доходов frontier LLM-лабораторий: сходится ли подписочная и enterprise арифметика (OpenAI, Anthropic, xAI, Mistral, Perplexity, Cohere)
session_id: unknown
machine: NODE-0X-2023PAL
targets: chatgpt,gemini,grok,claudeai,glm,claudecli
---

# Forensic investigation: are the headline revenues of frontier LLM labs arithmetically possible?

You are a forensic financial analyst in the tradition of short-seller research desks
(Muddy Waters, Hindenburg, Kynikos) and of accounting sceptics like Francine McKenna
and the FT Alphaville / Bethany McLean school. Your job is NOT to cheer and NOT to
debunk. Your job is to rebuild the revenue of AI labs BOTTOM-UP from unit economics
and check whether the top-down numbers the market repeats can actually exist.

Think as deeply and as long as you can. Turn on the strongest reasoning / deep-research
mode available in this account. I need a maximally thorough, sourced, dated answer with
explicit confidence levels and explicit gaps.

## The claim under test (treat as a hypothesis to falsify, not a conclusion)

H1 (subscriptions): consumer subscriptions cannot carry the reported revenue, because
the paid-conversion rate on freemium AI chat products is low (order of 3-10% of MAU,
possibly lower), the $100-250/month tiers are a very thin sliver (order of tenths of a
percent to low single-digit percent of paying users), and the blended ARPU is therefore
far below what a naive "N million users x $20" arithmetic implies.

H2 (enterprise): "enterprise revenue" is being inflated by (a) counting bookings, ACV,
TCV, RPO or non-binding LOIs as revenue; (b) a small number of very large contracts
(including related-party or investor-affiliated ones) doing most of the work;
(c) credits, discounts and compute-for-equity round-tripping. To produce $1B+ of real
annualised enterprise revenue you need hundreds of seven-figure accounts, and the
enterprise software market historically produces that cohort slowly.

H0 (null / the steelman you MUST also argue): the reported numbers are broadly real.
API + enterprise seats + government contracts + a genuinely unprecedented consumer
conversion curve can produce them. Argue this case as hard as you argue H1/H2, and say
which side the evidence actually favours.

## Companies (cover at least 6; run each as its own case file)

1. OpenAI
2. Anthropic
3. xAI
4. Mistral AI
5. Perplexity
6. Cohere
Plus, as CALIBRATION ANCHORS (they file audited numbers, so they bound what is
plausible): Microsoft's AI/Copilot disclosures, Alphabet/Google Cloud + Gemini,
and at least one mature SaaS comparable (e.g. Salesforce, Datadog, Snowflake) for
how fast a company historically reaches N hundred seven-figure logos.

## What each case file must contain

A. **Revenue decomposition.** Split every reported figure into: consumer subscription /
   prosumer high tier / API usage / enterprise seats & platform / government & defence /
   licensing & other. Where the split is not disclosed, say so and give your estimated
   split with a stated method.

B. **Bottom-up subscription model.** Build the arithmetic explicitly:
   MAU or WAU (source + date) -> paying conversion % -> tier mix ($20 vs $100-250) ->
   churn -> blended ARPU -> implied subscription revenue. Show the range (bear / base /
   bull) and compare it with what the company or its leaks claim. Name the single
   assumption that the answer is most sensitive to.

C. **Bottom-up enterprise model.** How many paying enterprise accounts would be needed
   at what average contract value to produce the claimed enterprise line? Then go find
   how many named, verifiable large customers actually exist (press releases, case
   studies, procurement records, USASpending / TED / GOV.UK contract registers, SEC
   filings of the CUSTOMER side, which are often the only audited evidence). Compare
   the required count with the observable count and quantify the gap.

D. **Definitional forensics.** For every headline number, establish which metric it
   actually is: GAAP revenue, annualised run-rate (ARR) from a single good month or
   week, bookings, RPO, gross vs net of inference cost, gross vs net of revenue share
   with a cloud partner, or a journalist's paraphrase of an unnamed source. Flag
   annualisation of a peak month, and flag any number that traces back to a single
   anonymous press report that everyone then re-cited (citation laundering).

E. **Related-party and circular-flow analysis.** Map compute-for-equity, vendor
   financing, investor-customers, and cloud-credit round-trips. Where an investor is
   also a large customer, quantify how much of the revenue line that relationship could
   explain.

F. **Cash vs revenue.** Revenue claims are cheap; cash burn is not. Estimate gross
   margin after inference cost, and reconcile the revenue story with the size and
   frequency of the funding rounds. A company raising every few months at a rising
   valuation while claiming rapid revenue growth is a specific, testable pattern:
   test it.

G. **Falsification list.** For each company list the 3-5 specific facts that, if found,
   would DISPROVE your conclusion, and say whether you looked for them and what you found.

## Evidence rules (non-negotiable)

- Cite a source and a DATE for every number. Prefer, in order: audited filings of the
  company or of its counterparties; regulatory and procurement registers; court and
  litigation exhibits; primary company disclosures; reputable investigative press with
  named documents; then everything else.
- Distinguish MEASURED from ESTIMATED from ASSERTED. Mark each number.
- Two sources agreeing does NOT confirm a fact if both trace to the same origin.
  Explicitly check for shared provenance before calling anything corroborated.
- Say plainly where the data does not exist. "I could not find it" is a valid and
  valuable answer; do not fill gaps with plausible-sounding numbers.
- Note your training-data cutoff and mark which parts of the answer may be stale.

## Deliverable

1. One-page verdict: for each company, a score on "reported revenue is plausible
   bottom-up" (1-5) with the single strongest piece of evidence for and against.
2. A comparison table across all companies: claimed revenue, bottom-up reconstructed
   range, gap, dominant revenue source, biggest unverifiable component.
3. The three specific numbers that, if any regulator or journalist obtained them,
   would settle the question fastest - and where those numbers physically live.
4. An explicit statement of which of H1 / H2 / H0 the evidence supports, per company
   and overall, with your confidence level.

Internal analysis, not for publication. Be blunt.


===== VENDOR: report (DR26-09-14-ZB-09-2008-claudecli.md) =====
Note before I start: my model training cutoff is January 2026. Everything dated after that — i.e. most of the specific 2026 figures below — comes from live web search run just now, not from memory. That matters forensically: the private-company numbers are almost all **un-audited secondary reporting**, and I will mark them as such. The only genuinely audited numbers in this whole exercise are the calibration anchors (Microsoft, Alphabet) and one litigation-adjacent filing (SpaceX's S-1, which consolidates xAI). Treat the private-lab precision as illusory.

---

# FORENSIC INVESTIGATION: ARE FRONTIER-LAB REVENUES ARITHMETICALLY POSSIBLE?

## PREAMBLE — the meta-finding that governs every case file

Before any single company: the **provenance structure** of this entire dataset is the story. I traced the sourcing chain on every headline number I could, and the pattern is consistent and damning for anyone who wants precision:

- **~4 primary origins carry the entire narrative.** (1) *The Information* (subscriber-shared documents, run-rate leaks, burn figures); (2) *Bloomberg* (circular-deal mapping, the $40B OpenAI run-rate); (3) *Ramp* corporate-card spend data (customer concentration); (4) *Menlo Ventures* enterprise-adoption survey (market share). Almost every other number is downstream of these.
- **A dense layer of citation-laundering sits on top.** Domains like getpanto.ai, valueaddvc.com, aibusinessweekly.net, axis-intelligence.com, useluminix.com, sacra.com, etc. re-publish the same 4 origins with added false precision and no new evidence. Two of them "agreeing" confirms nothing — I checked, and they share provenance. **I discount them to zero as independent corroboration.** [MEASURED: I opened the search result sets; the same figures recur verbatim across domains.]
- **The labs are private.** None of OpenAI, Anthropic, xAI, Mistral, Perplexity or Cohere files audited financials. Every "$X billion ARR" is either (a) self-reported by the company to press/investors, or (b) leaked from an investor deck. **None is GAAP revenue verified by an auditor.** The word "revenue" in these headlines is doing work it has not earned.

That is the null result you should hold onto: **for the six labs, the top-down numbers cannot be independently confirmed at all**, and the bottom-up reconstructions below are the *only* discipline available. Where they reconcile, I say so. Where they don't, I say that louder.

---

## CASE FILE 1 — OpenAI

### A. Revenue decomposition
Headline: **run-rate "$40B+" as of Aug 2026** [ASSERTED → Bloomberg, 2026-08-13, "OpenAI's Revenue Run Rate Tops $40 Billion Ahead of IPO"], up from ~$25B ARR (Feb–Mar 2026) and ~$10B (Jun 2025). A leaked August breakdown circulated as: ~$22B ChatGPT subscriptions, ~$12B API, ~$6B Sora/ads/licensing [ASSERTED, single leaked breakdown, un-named deck]. The company also claims **enterprise now >40% of revenue, crossing consumer parity** [ASSERTED, company statement].

Critical definitional flag: **"$40B" is an annualized run-rate, not a fiscal-year revenue.** The audited-adjacent number that exists is *actual* H1 2025 revenue ≈ **$4.3B** [ASSERTED → Reuters relaying The Information] and Q1 2026 revenue **$5.7B with $3.7B cash burn** [ASSERTED → The Information, "OpenAI Burned $3.7 Billion in First Three Months of 2026," shared shareholder documents]. Q1 2026 × 4 ≈ $23B — i.e. the run-rate more than doubling to $40B in five months requires accepting a July "+20% MoM" spike [ASSERTED → Bloomberg] annualized off a single strong month. **That is textbook peak-month annualization.**

### B. Bottom-up subscription model
Inputs: WAU **900M** (Mar 2026) [ASSERTED]; paying consumer subs **"50M+"** (OpenAI COO) [ASSERTED, no date-stamped audit]; tier split — the widely-repeated "5.8% Pro" figure is **5.8% of consumer *revenue*, Jan 2025**, not 5.8% of users [MEASURED: this is the actual claim; the blogs mis-derived "2.9M Pro users"].

Correcting that error is the whole ballgame. If Pro ($200) is 5.8% of revenue and Plus is $20:
- Solve for Pro user-share x: 200x / (200x + 20(1−x)) = 0.058 → **x ≈ 0.6% of paying users.** Pro is a *sliver*, exactly as H1 predicts.
- Blended monthly ARPU ≈ 0.994×$20 + 0.006×$200 = **~$21/mo**.

| Scenario | Paying subs | Blended ARPU/mo | Implied annual consumer sub revenue |
|---|---|---|---|
| Bear | 40M | $19 | **$9.1B** |
| Base | 50M | $21 | **$12.6B** |
| Bull | 55M | $24 (richer Team/Business mix) | **$15.8B** |

**Reconciliation:** pure Plus/Pro consumer reconstructs to **~$12–13B**, *not* the "~$22B ChatGPT subscriptions" leak. The $22B is only reachable if it bundles ChatGPT Team/Business/Enterprise *seats* into "subscriptions." So the leak isn't necessarily false — but it is **mislabeled**: it is not consumer freemium conversion, it is seat-based B2B wearing a consumer label. **H1 is directionally vindicated on the consumer line.**
Most sensitive assumption: **the paid-subscriber count (50M).** Everything keys off it, and it is a single un-audited executive assertion.

### C. Bottom-up enterprise model
Claimed enterprise ≈ >40% of $40B ≈ **$16B+** [ASSERTED]. Also "9M+ paying business users" [ASSERTED]. At ChatGPT Enterprise ~$60/seat/mo blended, 9M seats × $60 × 12 = **$6.5B** — so seat revenue alone doesn't reach $16B; the balance must be **API consumption** (developers, not seats). Cross-check: Ramp/Menlo data shows OpenAI + Anthropic together, and OpenAI's API is real and large. Observable named enterprise logos exist in abundance (this is OpenAI's genuine strength). **The gap here is smaller than for peers** — but note the concentration finding below.

### D. Definitional forensics
- "$40B" = run-rate off a peak month. **Flag.**
- "$22B subscriptions" = almost certainly bundles B2B seats. **Mislabel flag.**
- "$100M ads ARR in under six weeks" [ASSERTED → repeated] = six-week annualization, the most aggressive possible. **Flag.**

### E. Related-party / circular-flow
This is OpenAI's defining forensic risk. Mapped circular deals [ASSERTED → Bloomberg, "AI Circular Deals," 2026]: **Nvidia up to $100B into OpenAI ↔ OpenAI buys Nvidia chips; OpenAI–Oracle ~$300B; OpenAI–AMD (chips for up to 10% AMD stake, ~$300B purchase commitment).** Over **$800B** of intertwined vendor-financing across the ecosystem. None of this is *revenue* for OpenAI directly, but it means OpenAI's demand is partly **funded by its own suppliers**, and Microsoft is simultaneously OpenAI's largest investor and, via GitHub, a large *counterparty in Anthropic's* revenue. The revenue line is real API usage; the *sustainability* of the counterparties' spend is the circular question.

### F. Cash vs revenue
Q1 2026: **$5.7B revenue, $3.7B burn (65% of revenue)** [The Information]. Cash $73B end-Q1 (from $40B) — i.e. the burn is covered by *financing, not operations*. OpenAI's own forecast: **~$14B loss in 2026** [ASSERTED → Yahoo/report]. Gross margin after inference: undisclosed; the fact that they raise every few months at rising valuations while claiming hypergrowth is **exactly the testable pattern in the brief — and it tests positive.** Revenue growth is real; it is also *necessary* to service the compute commitments, which is a different thing from *profitable*.

### G. Falsification list
1. *Audited GAAP revenue showing $40B is real, not run-rate* — **looked; does not exist** (private). 
2. *Consumer subs materially above 55M at >$25 ARPU* — **looked; only 50M asserted.** Would raise my subscription plausibility. 
3. *Pro tier being a large user share* — **looked; it's ~0.6%.** Confirms H1. 
4. *Enterprise revenue net of Microsoft/related-party* — **not disclosed.** 
5. *A single audited quarter contradicting the $3.7B burn* — **none found; the burn number is the most credible figure OpenAI has, because it's the one that hurts.**

**Verdict OpenAI: revenue is largely REAL but the labels are inflated (run-rate-as-revenue, seats-as-subscriptions, peak-month annualization). Plausibility 4/5.**

---

## CASE FILE 2 — Anthropic

### A. Revenue decomposition
Headline run-rate escalated absurdly fast in the reporting: ~$5B (Aug 2025) → "$14B" (Feb 2026) → "$30B" (Apr) → "$47B" (May) → **"$65B" (Jul 2026)** [all ASSERTED, secondary; the $65B from valueaddvc-tier sources — **low confidence, likely laundered**]. The most *load-bearing, best-sourced* figure is **$5B run-rate with ~80% from API/enterprise** [The Information; Menlo Ventures]. I trust the $5B-era decomposition far more than the $65B headline.

### B. Bottom-up subscription model
Anthropic is **~80% API/enterprise, ~20% consumer** [ASSERTED → repeated, Menlo]. Consumer (Claude.ai Pro/Max at $20/$100–200) is therefore *not* the story and cannot carry the number — which is *consistent* with H1, just via a different route: Anthropic doesn't pretend consumer carries it. Consumer ≈ 20% × $5B ≈ $1B, plausible at a few million Pro subs. **No inflation needed here; the model is honest about being enterprise-led.**

### C. Bottom-up enterprise model — THE KEY FINDING
[MEASURED-adjacent, best evidence in the entire report]: **Cursor + GitHub Copilot alone ≈ $1.2B of the ~$4–5B total — "nearly a quarter" from two customers** [The Information, relayed VentureBeat, 2026]. And **top 1% of customers = ~80% of enterprise revenue** [Ramp research]. Claude Code itself ≈ $400M annualized [The Information].

This is **H2 confirmed in its strongest form.** The enterprise line is real revenue but **radically concentrated**: you do *not* need "hundreds of seven-figure logos" because a handful of AI-coding customers (themselves VC-funded, themselves burning cash, one of them — GitHub — owned by Microsoft, which funds OpenAI) do the work. The forensic risk isn't fabrication; it's **fragility**: if Cursor's economics break or Copilot re-routes to an in-house/OpenAI model, ~25% of revenue moves. Ex-those-two, the rest grew "11-fold YoY" [The Information] — genuinely fast, but off a small base.

### D. Definitional forensics
The $5B→$65B ramp in ~11 months is the reddest flag in the sector. $5B and the concentration data are well-sourced. **$30B/$47B/$65B are single-report or laundered and I mark them LOW confidence.** The pattern "run-rate re-quoted upward monthly" is precisely the peak-annualization risk.

### E. Related-party / circular-flow
Less capex-circular than OpenAI, but note: **a quarter of revenue flows through two apps, one (GitHub) owned by Microsoft** [theclarity.us, 2026-09-06, relaying the same data]. Amazon and Google are both large *investors* and *cloud providers* — compute-for-equity dynamics apply (Anthropic's costs and one funding source are the same entity).

### F. Cash vs revenue
Anthropic claims approaching profitability / "first profit" in some 2026 reports [ASSERTED, LOW confidence]. Given 7× Claude-Opus token pricing vs GPT-5 [VentureBeat] and enterprise mix, gross margins *could* be better than OpenAI's — but a **pricing war explicitly threatens margins** [VentureBeat headline]. Undisclosed and unverifiable.

### G. Falsification list
1. *Concentration is NOT real (broad customer base)* — **looked; Ramp + The Information both say 80%/top-1%. Concentration confirmed.** 
2. *$65B run-rate has a primary source* — **looked; could not find one that isn't laundered.** 
3. *Consumer is secretly large* — **no; ~20%.** 
4. *Cursor/Copilot $1.2B is double-counted* — **checked; reported as direct API spend, not double-counted.** 
5. *Margins are positive after inference* — **not disclosed.**

**Verdict Anthropic: the $5B-era number is REAL but H2-concentrated to an extreme; the $30–65B headlines are UNVERIFIED and likely run-rate inflation. Plausibility of the *headline* 2/5; plausibility of *"real enterprise revenue exists, just concentrated"* 4/5.**

---

## CASE FILE 3 — xAI

### A/D. Revenue decomposition & definitional
Grok/xAI AI revenue ≈ **$500M annualized (mid-2026)**, up from ~$350M (2025) [ASSERTED → Sacra, secondary]. Consolidated with X's ad/subscription revenue, "$3.3B+ annualized by year-end" [ASSERTED] — but that **bundles X (Twitter) advertising into "AI revenue,"** which is a category error. The AI-attributable line is the ~$500M.

### B. Subscription model
SuperGrok ~$30/mo, SuperGrok Heavy ~$300/mo [ASSERTED]. Even generously: to reach $500M *from subscriptions* you'd need ~1.4M SuperGrok-equivalent subs. Plausible only if distribution via X inflates conversion. The high tier ($300) is again a sliver. **H1 applies.**

### C/E/F. The forensic core — this one has an audited-adjacent number
**xAI burned $6.4B in a year; ~$1B/month burn against ~$500M ARR** [MEASURED-adjacent → SpaceX IPO/S-1 filing surfaced via Yahoo Finance/Bloomberg, 2026 — *this is the closest thing to an audited disclosure in the whole sector because it rides in SpaceX's filing*]. Net loss $1.46B in the Sept-2025 quarter alone. **On Feb 2, 2026, xAI merged into SpaceX (all-stock, ~$250B valuation)** [ASSERTED → repeated] — which is *itself* a forensic event: an unprofitable AI lab absorbed into a related private entity controlled by the same person, moving its financials off any standalone scrutiny. Prior: $20B Series E (Jan 2026, $230B valuation); ~$42B raised cumulatively.

Burn ÷ revenue ≈ **24×.** This is the worst revenue-quality profile of the six: the smallest verified revenue, the largest verified burn, and a related-party merger that removes standalone disclosure.

### G. Falsification list
1. *AI revenue is >$1B standalone* — **no evidence; ~$500M.** 
2. *Burn is overstated* — **the S-1 says $6.4B; it's the credible number.** 
3. *X ad revenue is legitimately AI* — **no; it's legacy Twitter.**

**Verdict xAI: AI revenue REAL but tiny (~$500M) and dwarfed by burn; "$3.3B" conflates X ads. Plausibility of the *AI* number 3/5; plausibility of the *conflated* number 1/5. H1 + cash-burn story strongly supported.**

---

## CASE FILE 4 — Mistral AI

### A/B/C/D
ARR trajectory: **€300M (Sep 2025) → ~$400M (Jan 2026)**, targeting **>€1B revenue by end-2026** [ASSERTED → Maddyness / Davos CEO statement; Sacra]. Revenue = enterprise licensing + Le Chat Enterprise + consumer Chat; **~60% from Europe** [ASSERTED]. Funding: €1.7B Series C (Sep 2025, ASML-led, €11.7B post) → **$3.5B at $20B (Jun 2026)** [ASSERTED].

Forensic read: the €300M→€1B *target* is a **projection, not a run-rate** — correctly labeled as a target by the CEO, which is more honest than peers. The €300M ARR is small enough to be plausibly enterprise-license-driven without needing a fantastical consumer curve. Biggest unverifiable: the **split between binding enterprise contracts and pipeline** — European licensing deals (sovereign-AI, ASML as strategic investor-customer) raise the **investor-customer** flag (ASML is both lead investor and a potential customer).

### E/F/G
Related-party: ASML investor-customer overlap [flag, unquantified]. Cash: undisclosed; €1.7B + $3.5B raised against ~$400M ARR implies heavy burn but far less extreme than xAI. Falsification: I looked for audited French filings (Mistral SAS accounts may eventually appear in French registres) — **not found in this run**; that is where the truth physically lives.

**Verdict Mistral: small, plausibly-real enterprise ARR, honestly labeled as a target. Plausibility 4/5. Least inflated of the group, mostly because the numbers are small and the CEO says "target."**

---

## CASE FILE 5 — Perplexity

### A/B/C/D
ARR **~$100M (early 2025) → >$450M (Mar 2026)**, targeting $656M by year-end [ASSERTED → repeated, FT relayed for the 100M MAU figure]. **100M+ MAU** (FT, Apr 2026, *with agents included* — a definitional softener) [ASSERTED]. Paid users: **not disclosed; ~1M estimated** [ESTIMATED → Resourcera calculation, weak].

The forensic tell: **"$450M ARR — a 50% jump in a single month" driven by a Feb-25 product launch** [ASSERTED]. That is peak-month annualization stated openly. At ~1M paid users × ~$20/mo × 12 = **$240M** — so the reconstructed subscription line is **roughly half** the claimed $450M ARR, meaning the balance is **usage-based/agent/API** revenue annualized off a spike. **H1 applies to the subscription half; the other half is annualized new-product revenue that has not proven durable.**

### E/F/G
Perplexity is a **reseller of others' models** — its COGS is API payments to OpenAI/Anthropic/Google, so gross margin is structurally thin and its "revenue" partly round-trips to competitors. Raised repeatedly at soaring valuations ($23B/$20B range, 2026) against <$500M ARR — the raise-often-while-claiming-growth pattern **tests positive**. Falsification: *a disclosed paid-subscriber count* would settle it — **does not exist.**

**Verdict Perplexity: real but small (~$240M reconstructable, $450M claimed via annualized spike); thin-margin reseller. Plausibility 3/5. H1 supported.**

---

## CASE FILE 6 — Cohere

### A/B/C/D
**$240M ARR (2025), +287% YoY from $62M (end-2024)**, beating a $200M internal target [ASSERTED → CNBC "Cohere tops revenue target," 2026-02-13, investor memo — *relatively well-sourced*]. **~85% from private deployments**; named customers Oracle, Fujitsu, RBC, LG, Notion on multi-year contracts [ASSERTED]. But note the tension: **SeekingAlpha (2025) reported annualized revenue at just ~$70M** at one point [ASSERTED → SeekingAlpha], vs the $240M year-end. That's a wide intra-year spread — consistent with a small number of large contracts landing lumpily (classic enterprise), *and* consistent with run-rate volatility.

### C — enterprise reconstruction
$240M with ~85% private-deployment across named logos like Oracle/RBC/Fujitsu implies **a handful of seven-/eight-figure deals**, not hundreds. Verifiable named customers *exist and are nameable* — better than most peers — but the count is **small**, so concentration risk is high (H2-style, but disclosed).

### E/F/G
**Nvidia-backed** [ASSERTED] — investor-supplier overlap. Valuation $7B (Sep 2025) against $240M ARR = ~29× ARR. Falsification: *contract-level ACV disclosure* would settle concentration — not public. The $70M vs $240M discrepancy is the thing I'd most want reconciled.

**Verdict Cohere: smallest and arguably cleanest — nameable enterprise logos, a CNBC-sourced beat, honest "private deployment" framing. Plausibility 3.5/5. H2-concentration present but disclosed, not hidden.**

---

## CALIBRATION ANCHORS (audited — these bound what's plausible)

**Microsoft** [MEASURED → SEC filings / IR]: AI run-rate **$13B (disclosed FY25 Q2, Jan 2025), then the metric was withdrawn from disclosure** — itself a tell; reportedly ~$37B run-rate by FY26 Q3 [ASSERTED, no longer formally disclosed]. **M365 Copilot >30M paid seats (FY26 Q4)** [MEASURED-adjacent, IR]. Capex guided to **$190B+** — the demand that funds the labs' revenue is the same hyperscaler capex cycle.

**Alphabet** [MEASURED → SEC 8-K, Q2 2026, googexhibit991q22026.htm]: total revenue **$119.8B**, **Google Cloud $24.8B (+82%)**, **cloud backlog $514B (RPO), ~50% to convert within 24 months**, cloud operating margin 35.6%. **Gemini app 950M active users.** This is what audited AI-adjacent scale looks like: RPO is disclosed *as backlog, not as revenue* — exactly the discipline the private labs lack. Google booking $514B of backlog and still only recognizing ~half within 2 years shows how *slowly* even real enterprise commitments convert to revenue — a direct rebuke to private "run-rate = revenue" framing.

**SaaS comparable (Salesforce)** [MEASURED → SEC filings]: took **~10 years to reach $1B** revenue; "fastest ever to $5B" was still ~15 years in. The historical enterprise-software cohort of seven-figure logos accumulates over **years**, not months. When a private lab claims to add tens of $B of "enterprise ARR" in under a year, it is either (a) a genuinely unprecedented curve, or (b) not measuring GAAP enterprise revenue. The anchor says: **be very suspicious of (a).**

---

## DELIVERABLE 1 — ONE-PAGE VERDICT (plausibility 1–5, bottom-up)

| Company | Score | Strongest FOR | Strongest AGAINST |
|---|---|---|---|
| **OpenAI** | **4/5** | Q1'26 $5.7B rev / $3.7B burn shared to shareholders (the painful number is credible); real API + 50M subs | "$40B" is peak-month run-rate; "$22B subscriptions" bundles B2B seats |
| **Anthropic** | **2/5 headline, 4/5 core** | Cursor+Copilot $1.2B and 80%/top-1% concentration are Ramp+TI-sourced (real revenue) | $30B→$65B ramp has no primary source; extreme 2-customer fragility |
| **xAI** | **3/5 AI-line, 1/5 headline** | $6.4B burn rides SpaceX's S-1 (near-audited) | ~$500M AI ARR vs ~$1B/mo burn; "$3.3B" conflates X ads; merged out of view |
| **Mistral** | **4/5** | CEO labels €1B as a *target*, not run-rate; €300M ARR small & enterprise-plausible | ASML investor-customer overlap; no audited French accounts found |
| **Perplexity** | **3/5** | $100M→$450M growth is real directionally | $450M = 50%-in-one-month annualized spike; thin-margin reseller; ~$240M reconstructable |
| **Cohere** | **3.5/5** | CNBC investor-memo $240M beat; nameable logos (Oracle/RBC/Fujitsu) | $70M vs $240M intra-year spread; tiny logo count = concentration |

---

## DELIVERABLE 2 — COMPARISON TABLE

| Company | Claimed (date, type) | Bottom-up reconstructed range | Gap | Dominant real source | Biggest unverifiable component |
|---|---|---|---|---|---|
| OpenAI | $40B run-rate (Aug'26) | Consumer $9–16B + API/ent. $16–24B ≈ **$25–40B** | Consumer line ~$9B *below* the "$22B subs" label | ChatGPT subs + API | Enterprise net of Microsoft/related-party; peak-month portion |
| Anthropic | $5B (well-sourced) → $65B (laundered) | **$4–6B** defensible | $30–65B **unverified** | Enterprise API (coding) | Any run-rate above ~$6B; margin after inference |
| xAI | $500M AI / $3.3B consolidated | **~$500M** AI | $2.8B = X ads, not AI | Grok subs + X (legacy) | AI-vs-legacy split post-SpaceX merger |
| Mistral | €1B *target* / €300–400M ARR | **~$400M** | Target ≠ current (honest) | Enterprise licensing (EU) | Binding contracts vs pipeline; ASML overlap |
| Perplexity | $450M ARR (Mar'26) | **~$240M** subs + agent spike | ~$210M is annualized new-product | Consumer subs | Paid-sub count (undisclosed); reseller margin |
| Cohere | $240M ARR (2025) | **$70–240M** (lumpy) | Intra-year $170M swing | Private enterprise deployments | ACV per contract; logo count |
| *MSFT (anchor)* | *$13B→$37B (audited then withdrawn)* | *n/a — audited* | *—* | *Copilot seats + Azure AI* | *Metric withdrawal itself* |
| *Alphabet (anchor)* | *Cloud $24.8B/qtr, $514B RPO (audited)* | *n/a — audited* | *—* | *Cloud + Gemini* | *— (properly disclosed)* |

---

## DELIVERABLE 3 — THE THREE NUMBERS THAT WOULD SETTLE IT, AND WHERE THEY PHYSICALLY LIVE

1. **OpenAI's audited GAAP full-year revenue and its consumer-vs-enterprise-vs-API split, net of Microsoft-related-party transactions.** Lives in: the **S-1 registration statement** OpenAI must file with the **SEC** ahead of the widely-reported IPO. This single document collapses the run-rate/seats/subscriptions ambiguity instantly. Until it's filed, everything is a leak.
2. **Anthropic's revenue net of its top ~10 customers (especially Cursor and GitHub/Microsoft), with contract terms.** Lives in: **Anthropic's investor data room / Ramp's underlying anonymized card-spend panel**, and would surface in any **Anthropic S-1** or in **Microsoft's / a customer's own audited segment disclosure**. The concentration is the whole risk; the de-concentrated number is the truth.
3. **xAI's standalone AI-only revenue and burn, separated from X advertising, post-SpaceX merger.** Lives in: the **SpaceX S-1 / audited consolidated financials** (SpaceX is heading toward disclosure; xAI now consolidates into it). This is the *only* one of the three that partially exists already — the $6.4B burn came from exactly this filing — which is why xAI's cash story is the best-evidenced and worst-looking.

Secondary settling numbers, by physical location: **French registre du commerce** (Mistral SAS statutory accounts); **USASpending.gov / SAM.gov / FPDS** and **UK Contracts Finder / TED** (government seats for OpenAI/Anthropic — the audited *customer* side); **Microsoft & Alphabet 10-Ks** (their disclosed AI run-rates bound the whole market from above).

---

## DELIVERABLE 4 — WHICH OF H1 / H2 / H0 THE EVIDENCE SUPPORTS

**Per company:**
- **OpenAI** → **H0-leaning** (revenue broadly real) **but with H1 label-inflation**: subscriptions *are* a big real line, yet "$22B subscriptions" smuggles B2B seats and "$40B" is run-rate. The high tier (Pro) is genuinely a ~0.6% sliver — H1's specific claim is *correct*. Confidence: **Medium-High.**
- **Anthropic** → **H2 confirmed, strong form**: real enterprise revenue, but ~25% from two customers and 80% from the top 1%. Not fabricated, but exactly the "small number of very large contracts doing the work" thesis. The $30–65B headlines are **unverified**. Confidence: **High** on concentration, **High** that the top-end headline is inflated.
- **xAI** → **H1 + cash-burn thesis**: tiny AI subscription revenue, gigantic burn, and "$3.3B" is achieved only by conflating legacy X advertising. Confidence: **High.**
- **Mistral** → **H0** (the cleanest): small, plausibly-real, honestly labeled as a *target*. No inflation detected. Confidence: **Medium** (small numbers, thin disclosure).
- **Perplexity** → **H1** (subscription half real, other half annualized spike) **+ thin-margin reseller** risk. Confidence: **Medium-High.**
- **Cohere** → **H2-mild but disclosed**: real, nameable enterprise deals, concentrated in few logos, honestly framed. Confidence: **Medium.**

**Overall verdict (blunt):**
The evidence supports **a blend of H0 and H2, with H1 vindicated on the specific consumer-arithmetic claims.** Namely:
- **H1 (subscriptions can't carry it) — SUPPORTED as stated.** The $100–250 tiers really are sub-1% slivers (OpenAI Pro ~0.6%; SuperGrok Heavy, Claude Max, Perplexity Max all tiny). Blended consumer ARPU sits near **$20–21**, and pure consumer freemium reconstructs to a fraction of headline "subscription" lines. Where labs *label* seat-based B2B as "subscriptions," they mask this. **Confidence: High.**
- **H2 (enterprise inflated by concentration & definition) — SUPPORTED, strongest at Anthropic.** The enterprise revenue is *real* but produced by **a handful of very large, often investor-/supplier-adjacent accounts**, not the "hundreds of seven-figure logos" a mature-SaaS lens expects — and the Salesforce/Alphabet anchors show that cohort takes *years*, not months, to build. Plus pervasive **run-rate-as-revenue** and **peak-month/peak-week annualization**. **Confidence: High.**
- **H0 (numbers broadly real) — PARTIALLY SUPPORTED, and this is the honest steelman:** the *underlying usage* is genuinely unprecedented. Alphabet's audited **$514B cloud RPO** and **950M Gemini users**, Microsoft's **30M+ Copilot seats**, OpenAI's **credible $5.7B/quarter with $3.7B burn** — these are real, audited-or-painful numbers showing demand that *no prior software cycle matched*. The labs are not Enron; they are not booking phantom revenue. **What they are doing is presenting run-rates, bookings-flavored ARR, and seat-bundles in the most flattering framing available for a private company that never has to reconcile to an auditor.** **Confidence: Medium-High.**

**The one-sentence forensic bottom line:** The *cash going in* is audited and enormous; the *revenue coming out* is real but **systematically over-labeled** — run-rate dressed as revenue, seats dressed as subscriptions, two customers dressed as a market, and peak months dressed as years — and because all six labs are private, **the single document that would end every argument (an SEC S-1) does not yet exist for any of them.** Until OpenAI's or Anthropic's S-1 lands, the correct analyst posture is: *believe the burn, discount the run-rate, and never call two blogs a corroboration.*

**Staleness caveat:** My training ends Jan 2026; all post-Jan-2026 figures above are from live search of an ecosystem dominated by ~4 primary sources and heavy citation-laundering. I have flagged every ASSERTED/ESTIMATED/MEASURED accordingly. The audited anchors (Alphabet 8-K, SpaceX S-1-derived burn, Microsoft IR) are the parts you can most trust; the private-lab run-rates are the parts you should trust least.

**Sources (opened this run):**
- [Bloomberg — OpenAI run-rate tops $40B](https://www.bloomberg.com/news/articles/2026-08-13/openai-s-revenue-run-rate-tops-40-billion-ahead-of-ipo)
- [The Information — OpenAI burned $3.7B in Q1 2026](https://www.theinformation.com/articles/openai-burned-3-7-billion-first-three-months-2026)
- [Reuters via TradingView — OpenAI H1 2025 revenue ~$4.3B](https://my.tradingview.com/news/reuters.com,2025:newsml_L3N3VH0A8:0-openai-s-first-half-revenue-rises-16-to-about-4-3-billion-the-information-reports)
- [VentureBeat — Anthropic revenue tied to two customers](https://venturebeat.com/ai/anthropic-revenue-tied-to-two-customers-as-ai-pricing-war-threatens-margins)
- [PYMNTS — OpenAI & Anthropic 80% revenue from 1% of customers](https://www.pymnts.com/news/artificial-intelligence/2026/openai-and-anthropic-get-80percent-of-revenue-from-1percent-of-customers/)
- [Bloomberg — AI circular deals graphic](https://www.bloomberg.com/graphics/2026-ai-circular-deals/)
- [Yahoo Finance — xAI burned $6.4B (SpaceX IPO filing)](https://finance.yahoo.com/sectors/technology/articles/xai-burned-6-4b-last-222608682.html)
- [StartupHub — xAI $500M ARR vs $1B monthly burn](https://www.startuphub.ai/ai-news/ai-figures/2026/figure-elon-musk-spacexai-financial-breakdown-2026-07-09)
- [Maddyness — Mistral on track for €1B by 2026](https://www.maddyness.com/uk/2026/01/23/mistral-ai-on-track-to-reach-one-billion-euros-in-revenue-by-2026/)
- [Sacra — Mistral revenue/valuation](https://sacra.com/c/mistral/)
- [FT-relayed / getpanto — Perplexity 100M MAU, $450M ARR](https://www.getpanto.ai/blog/perplexity-ai-statistics)
- [CNBC — Cohere tops revenue target ($240M), IPO momentum](https://www.cnbc.com/2026/02/13/ai-startup-cohere-revenue-ipo.html)
- [SeekingAlpha — Cohere annualized revenue ~$70M (earlier)](https://seekingalpha.com/news/4412490-cohere-annualized-revenue-hits-70m-as-it-focuses-on-enterprise-ai-report)
- [Alphabet Q2 2026 8-K (SEC)](https://www.sec.gov/Archives/edgar/data/id_1aeeedd0/000165204426000066/googexhibit991q22026.htm)
- [Microsoft FY26 Q3 earnings (IR)](https://www.microsoft.com/en-us/investor/earnings/fy-2026-q3/productivity-and-business-processes-performance)
- [IntuitionLabs — ChatGPT Free/Plus $20/Pro $200 tiers](https://intuitionlabs.ai/articles/chatgpt-plans-comparison)
- [Salesforce SEC 8-K filings (revenue milestones)](https://www.sec.gov/Archives/edgar/data/id_6c6d7d91/000110852415000011/crm-q1exhibit991.htm)


===== VENDOR: report (DR26-09-14-ZB-09-2008-gemini-cli.md) =====
llm_ask: ответила рельса gemini за 92s
# Forensic Financial Analysis: Reconstructing the Revenue of Frontier AI Labs

---

## SECTION 1: Calibration Anchors & Benchmarks

To establish what is arithmetically and operationally plausible, we first establish benchmark data from audited SEC filings and mature software-as-a-service (SaaS) historical trajectories.

```
+----------------------------------------------------------------------------------------------------+
|                                    SaaS ARR Growth Benchmark                                       |
|                                                                                                    |
|  ARR  ^                                                                                            |
| $1.0B |------------------------------------------------------------- [Snowflake: ~7.5 Yrs]         |
|       |                                                               [Datadog:   ~9.0 Yrs]        |
|       |                                                               [OpenAI:    ~1.5 Yrs]*       |
| $500M |                                                               [Anthropic: ~2.5 Yrs]*       |
|       |                                                                                            |
| $100M |----------------------- [Snowflake: ~5.0 Yrs]                                             |
|       |                         [Datadog:   ~6.0 Yrs]                                              |
|       +------------------------------------------------------------------------------------> Time    |
|       0                         5                           10 Yrs                                 |
|                                                                                                    |
| *Note: OpenAI & Anthropic ARR curves reflect management-asserted/leaked annualized run-rates,      |
|  not audited annual GAAP revenues.                                                                 |
+----------------------------------------------------------------------------------------------------+
```

### Anchor 1: Microsoft Corporation (SEC Filings: 10-K FY24, 10-Q Q1/Q2 FY25)
*   **Azure AI / Copilot Disclosures:** In FY24 Q4 (ended June 30, 2024), Microsoft disclosed that Azure AI services contributed 8 percentage points of growth to Azure’s 29% YoY revenue growth `[MEASURED: SEC Form 10-K, July 30, 2024]`. In FY25 Q1 (quarter ended Sept 30, 2024), AI contributed 12 percentage points of growth to Azure’s 33% growth `[MEASURED: SEC Form 10-Q, Oct 30, 2024]`.
*   **Quantitative Conversion:** Azure revenue is estimated by consensus at ~$75B annualized in mid-2024. A 12 percentage point contribution to growth implies an Azure AI annualized run-rate of approximately **$3.0B–$4.0B** in late 2024 `[ESTIMATED]`. Crucially, this includes compute reselling for OpenAI API models hosted on Azure, third-party models, and native Azure AI services.
*   **M365 Copilot Adoption:** Microsoft claimed over 60% of Fortune 500 companies purchased M365 Copilot seats by mid-2024 `[ASSERTED: Earnings Call, July 30, 2024]`. However, seat deployment counts remain undisclosed. Microsoft reported M365 Commercial Cloud revenue of $33.7B in Q4 FY24 (`[MEASURED]`), with M365 Copilot ARR estimated by market analysts at **$300M–$600M** `[ESTIMATED]`, representing <1.5% seat penetration among commercial enterprise seats.

### Anchor 2: Alphabet Inc. (SEC Filings: 10-K FY24, 10-Q Q3 FY24)
*   **Google Cloud / Gemini Integration:** Google Cloud reported Q3 2024 revenue of $11.35B (up 35% YoY) with operating income of $1.58B `[MEASURED: SEC Form 10-Q, Oct 29, 2024]`. 
*   **AI Direct Revenue:** Alphabet CEO Sundar Pichai stated on the Q3 2024 earnings call that Gemini API calls via Vertex AI grew 14x over the prior 12 months, and that consumer subscription revenues (Google One + YouTube) crossed a $15B annual run-rate `[ASSERTED: Earnings Call, Oct 29, 2024]`. 
*   **Forensic Accounting Isolation:** Google does *not* break out Gemini standalone subscriptions (Google One AI Premium @ $19.99/mo) from YouTube Premium or Google One storage tiers in SEC filings. The $15B figure is a composite `[MEASURED]`. Estimated Gemini standalone subscription ARR is **$250M–$450M** `[ESTIMATED]`, based on Google One reaching 100M total subscribers in Feb 2024 `[ASSERTED: Sundar Pichai X post, Feb 9, 2024]`.

### Anchor 3: Mature SaaS Enterprise Benchmarking (Snowflake Inc. & Datadog Inc.)
To assess the structural feasibility of reaching $1B+ enterprise ARR, we benchmark the timeline required to scale 7-figure ($1M+ ACV) enterprise accounts:

```
+----------------------------------------------------------------------------------------------+
| Benchmark Metric           | Snowflake Inc. (SNOW)       | Datadog Inc. (DDOG)               |
+----------------------------+-----------------------------+-----------------------------------+
| Years from $0 to $100M ARR | ~5.0 Years (FY15 -> FY20)   | ~6.0 Years (2012 -> 2018)         |
| Years from $100M to $1B    | ~2.5 Years (FY20 -> FY23)   | ~3.0 Years (2018 -> 2021)         |
| $1M+ ACV Customers at $1B  | 271 customers               | 216 customers                     |
|  ARR Threshold             | `[MEASURED: FY22 SEC 10-K]` | `[MEASURED: FY21 SEC 10-K]`       |
| Blended Enterprise Net     | 160%–178%                   | 130%–145%                         |
|  Expansion Rate (NDR)      | `[MEASURED]`                | `[MEASURED]`                      |
+----------------------------+-----------------------------+-----------------------------------+
```

**Forensic Takeaway from Anchors:** In historical software business models, generating $1B in pure enterprise SaaS revenue requires **200 to 300 named customers paying over $1M/year**, supported by net retention rates (NDR) exceeding 130%. If an AI lab claims $1B in enterprise ARR with fewer than 100 verifiable $1M+ accounts, it is either counting non-SaaS usage/burst API capacity, misclassifying prosumer seats, or recognizing gross gross-booking contracts before delivery.

---

## SECTION 2: Case Files — Frontier LLM Labs

---

### CASE FILE 1: OpenAI, LLC / OpenAI Global LLC

#### A. Headline Claims vs. Definitional Forensics
*   **Headline Assertions:** 
    *   $2.0B ARR achieved in Dec 2023 `[ASSERTED: *Financial Times* / *The Information*, Feb 2024]`.
    *   $3.7B ARR achieved in Aug 2024; $4.0B estimated end-2024 `[ASSERTED: *New York Times*, Sept 27, 2024, citing internal financial pitch deck]`.
    *   Targeting $11.6B revenue in FY2025 `[ASSERTED: *New York Times*, Sept 27, 2024]`.
*   **Provenance Chain:** The $3.7B run-rate figure originates from a single leaked investor presentation circulated during OpenAI’s $6.6B funding round in Sept/Oct 2024. Re-cited by Reuters, FT, Bloomberg without independent GAAP verification.
*   **Definitional Forensic:** The $3.7B is an **Annualized Run-Rate (ARR)** calculated by taking the single month of August 2024 revenue (~$308M) and multiplying by 12 `[ESTIMATED]`. It is **NOT GAAP Revenue**. Projected FY2024 full-year GAAP revenue was listed in the same pitch deck as **~$3.7B**, while reporting a net loss of **~$5.0B** after compute costs, stock compensation, and operating overhead `[ASSERTED: NYT, Sept 27, 2024]`.

```
                  OpenAI Revenue Decomposition (Aug 2024 ARR)
  
  Total Run-Rate: ~$3.70B / $308M Mo. Revenue
  +-----------------------------------------------------------------------------------+
  | Consumer Subscriptions (ChatGPT Plus/Team) : ~$2.70B (73%) [ESTIMATED]            |
  | API Usage Direct / Azure Enterprise Share  : ~$0.75B (20%) [ESTIMATED]            |
  | ChatGPT Enterprise / Edu Direct Seats      : ~$0.25B ( 7%) [ESTIMATED]            |
  +-----------------------------------------------------------------------------------+
```

#### B. Bottom-Up Consumer Subscription Model
*   **Data Inputs:** 
    *   Weekly Active Users (WAU): 250M `[ASSERTED: OpenAI Press Release, Aug 2024]`; 350M `[ASSERTED: Sam Altman X post, Nov 2024]`.
    *   Estimated Monthly Active Users (MAU): ~350M–400M in late 2024 `[ESTIMATED]`.
    *   Paid Subscribers: Leaked pitch deck indicated ~10M paying ChatGPT Plus subscribers @ $20/mo in mid-2024 `[ASSERTED: NYT / The Information, Sept 2024]`.
    *   ChatGPT Pro Tier ($200/mo) launched Dec 2024 `[MEASURED: OpenAI Launch, Dec 5, 2024]`.

*   **Bottom-Up Engine:**

$$\text{Sub Revenue} = \text{MAU} \times \text{Conversion \%} \times \left( (1 - \text{Mix}_{\text{Pro}}) \times \$20 + \text{Mix}_{\text{Pro}} \times \$200 \right) \times 12$$

```
+-------------------+--------------------+--------------------+--------------------+
| Parameter         | Bear Case          | Base Case          | Bull Case          |
+-------------------+--------------------+--------------------+--------------------+
| MAU               | 300,000,000        | 380,000,000        | 450,000,000        |
| Conversion %      | 2.2%               | 2.8%               | 3.3%               |
| Paying Users      | 6,600,000          | 10,640,000         | 14,850,000         |
| Tier Mix          | 99.8% $20 /        | 99.2% $20 /        | 98.5% $20 /        |
|                   | 0.2% $200          | 0.8% $200          | 1.5% $200          |
| Blended ARPU/mo   | $20.36             | $21.44             | $22.70             |
| Monthly Sub Rev   | $134.4M            | $228.1M            | $337.1M            |
| Implied Sub ARR   | $1.61 Billion      | $2.74 Billion      | $4.05 Billion      |
+-------------------+--------------------+--------------------+--------------------+
```

*   **Sensitivity & Assessment:** The model is most sensitive to **Conversion Rate of Free-to-Paid MAU**. A 50 bps drop in conversion collapses ARR by ~$450M–$600M. The Base Case ($2.74B) aligns with leaked pitch decks, verifying that **consumer subscriptions provide ~73% of total revenue**.

#### C. Bottom-Up Enterprise & API Model
*   **Enterprise Seats Claims:** OpenAI claimed 1,000,000 paying business seats across ChatGPT Enterprise, Team, and Edu `[ASSERTED: OpenAI Blog, Sept 2024]`.
*   **Seat ARPU:** ChatGPT Enterprise list pricing varies from $30 to $60/user/month depending on volume and contract term `[ESTIMATED]`. At a blended $35/user/month, 1.0M seats yield:

$$1,000,000 \times \$35 \times 12 = \mathbf{\$420M\text{ ARR}}$$

*   **Verifiable Corporate Customer Count:**
    *   *Publicly Confirmed Accounts:* PwC (100k seats deployed), Moderna (75k seats), T-Mobile, Morgan Stanley, Amgen, BNY Mellon `[MEASURED: Company Press Releases & Case Studies, 2023-2024]`.
    *   *Procurement / SEC Filing Verification:* Zero 10-K disclosures from customers list OpenAI as a material vendor (thresholds generally require material commitments >$50M+ or single-supplier concentration risk).
    *   *Gap Analysis:* To hit $1.0B in enterprise-only ARR, OpenAI requires ~2.3M corporate seats at $35/mo. The observable, announced seats across all press releases sum to ~350,000 seats `[ESTIMATED]`. The remaining 650,000 seats must reside in unannounced mid-market deployments or self-serve ChatGPT Team accounts.

```
+-----------------------------------------------------------------------------------+
| Enterprise Seat Gap Analysis                                                      |
| Required Seats for $1.0B Enterprise ARR :  2,380,000 seats                        |
| Claimed Total Business Seats            :  1,000,000 seats                        |
| Observable/Named Public Seats           :    350,000 seats                        |
| Unaccounted / Unannounced Deficit       :  2,030,000 seats                        |
+-----------------------------------------------------------------------------------+
```

#### D. Related-Party & Circular-Flow Analysis
*   **Microsoft Commercial Agreement:** Microsoft invested $13B in cash and cloud credits `[MEASURED: MSFT Form 10-K]`. OpenAI receives Azure compute credits; in exchange, Microsoft receives a 75% profit-share right until principal is repaid, then 49% of OpenAI Global LLC profits, plus a ~20% revenue share on OpenAI model usage commercialized through Azure `[ASSERTED: WSJ / NYT disclosures, 2023-2024]`.
*   **Circular Revenue Flow:**
    1.  Microsoft provides cash/credits to OpenAI.
    2.  OpenAI uses credits to buy compute on Azure (Recognized as Intelligent Cloud Revenue by Microsoft `[MEASURED]`).
    3.  Microsoft resells OpenAI API endpoints on Azure AI; OpenAI receives a share of this revenue.
    *   *Impact:* An estimated **$300M–$500M** of OpenAI's API run-rate is paid directly or indirectly by Microsoft enterprise customers via Azure commit drawdowns `[ESTIMATED]`.

#### E. Cash vs. Revenue & Unit Economics
*   **Compute Costs:** Leaked financial projections indicated compute costs (training + inference) for FY2024 were projected at **~$4.0B** `[ASSERTED: NYT, Sept 2024]`.
*   **Gross Margin Analysis:**
    *   ChatGPT Plus Subscriptions: Inference cost estimated at ~$0.04 per query (GPT-4o). At an average of 15 queries/day per power user (~450 queries/mo), inference cost is ~$18.00/user/mo against a $20 subscription. **Gross margin on power users is <10%** `[ESTIMATED]`.
    *   Light users subsidize power users; overall consumer gross margin estimated at **35%–45%** `[ESTIMATED]`.
    *   Net operational cash burn for FY24: **~$5.0B** on $3.7B revenue `[ASSERTED]`.

#### F. Falsification Criteria

```
+----------------------------------------------------------------------------------+
| OpenAI Falsification Audit                                                       |
+----------------------------------------------------------------------------------+
| Hypothesis / Fact to Disprove H1/H2         | Audit Result                       |
+---------------------------------------------+------------------------------------+
| 1. Form 10-K disclosure from Fortune 50     | UNVERIFIED: No US corporate 10-K   |
|    customer citing >$50M annual OpenAI      | filed in 2024 names OpenAI as a    |
|    licensing liability.                     | material operational contract.     |
| 2. Credit Card Transaction panel data       | PARTIALLY VERIFIED: YipitData /    |
|    showing ChatGPT Plus subscriber drop.    | ConsumerEdge data shows active paid|
|                                             | subs stabilized at 9M-11M range.   |
| 3. Microsoft Azure AI revenue breakdown     | VERIFIED: Azure AI 12% growth      |
|    showing zero third-party pass-through.   | contribution confirms substantial  |
|                                             | OpenAI API volume.                 |
+---------------------------------------------+------------------------------------+
```

---

### CASE FILE 2: Anthropic PBC

#### A. Headline Claims vs. Definitional Forensics
*   **Headline Assertions:** 
    *   $100M ARR in Dec 2023 `[ASSERTED: *The Information*, Dec 2023]`.
    *   $800M ARR projected by end of 2024 `[ASSERTED: *The Information*, May 2024]`.
    *   $1.0B ARR milestone crossed in late 2024 `[ASSERTED: Leaked investor briefings, Oct 2024]`.
*   **Definitional Forensic:** Unlike OpenAI, Anthropic’s business is heavily skewed toward API usage via cloud platform marketplaces (AWS Bedrock, GCP Vertex AI). The reported $1.0B ARR represents total annualized spend by end customers on Claude API models across direct endpoints and cloud reselling platforms `[ESTIMATED]`. It does **not** represent Anthropic’s net cash receipts if cloud platform commission cuts (typically 15–30%) are excluded.

```
                 Anthropic Revenue Decomposition ($1.0B ARR)
  
  Total Run-Rate: ~$1.00B
  +-----------------------------------------------------------------------------------+
  | API Usage via AWS Bedrock Marketplace       : ~$550M (55%) [ESTIMATED]            |
  | API Usage Direct (Anthropic Console) / GCP  : ~$250M (25%) [ESTIMATED]            |
  | Claude Pro / Claude Team Subscriptions      : ~$200M (20%) [ESTIMATED]            |
  +-----------------------------------------------------------------------------------+
```

#### B. Bottom-Up Consumer Subscription Model
*   **Data Inputs:** 
    *   Claude.ai web traffic: ~60M–80M monthly visits in late 2024 `[ESTIMATED: Similarweb data, Q3 2024]`.
    *   Estimated MAU: ~20M–25M `[ESTIMATED]`.
    *   Paid Conversion Rate: Estimated at 3.5%–4.5% due to high developer/technical user concentration relative to general consumers.

```
+-------------------+--------------------+--------------------+--------------------+
| Parameter         | Bear Case          | Base Case          | Bull Case          |
+-------------------+--------------------+--------------------+--------------------+
| MAU               | 18,000,000         | 24,000,000         | 30,000,000         |
| Paid Conversion % | 2.5%               | 3.8%               | 5.0%               |
| Paying Users      | 450,000            | 912,000            | 1,500,000          |
| Tier Mix ($20/mo) | 100%               | 100%               | 100%               |
| Blended ARPU/mo   | $20.00             | $20.00             | $20.00             |
| Monthly Sub Rev   | $9.0M              | $18.24M            | $30.0M             |
| Implied Sub ARR   | $108 Million       | $218 Million       | $360 Million       |
+-------------------+--------------------+--------------------+--------------------+
```

*   **Assessment:** Consumer subscriptions account for only **~20%** of Anthropic’s run-rate. Anthropic cannot rely on consumer subs to carry its valuation; it is structurally an API/B2B infrastructure provider.

#### C. Bottom-Up Enterprise & API Model
*   **Distribution Architecture:** Anthropic's multi-cloud strategy anchors on AWS Bedrock and GCP Vertex. 
*   **AWS Bedrock Dynamic:** Amazon invested $4.0B in Anthropic as a minority investor via convertible notes and equity `[MEASURED: Amazon SEC Form 10-K 2023 / 10-Q Q3 2024]`. In exchange, Anthropic selected AWS as its primary cloud provider and Trainium/Inferentia chip partner.
*   **Contractual Revenue Commitments:**
    *   Amazon enterprise agreement commits Amazon sales teams to push Claude via Bedrock.
    *   To achieve $550M in AWS Bedrock Claude run-rate, AWS enterprise customers draw down their AWS Enterprise Discount Program (EDP) commitments to consume Claude tokens.
*   **Observable Enterprise Customers:** Pfizer, Bridgewater Associates, Boston Consulting Group, Asana, GitLab, Midjourney `[MEASURED: AWS & Anthropic Public Case Studies, 2023-2024]`.

```
+-----------------------------------------------------------------------------------+
| AWS EDP / Token Consumption Mechanics                                            |
|                                                                                   |
| Enterprise Customer ---> $10M AWS EDP Commit ---> Consumes $3M Claude 3.5 Sonnet  |
|                                                          |                        |
|                                                          v                        |
| Anthropic Recognized ARR ($3M) <--- 80% Share <--- AWS Bedrock Platform ($3M)    |
+-----------------------------------------------------------------------------------+
```

#### D. Related-Party & Circular-Flow Analysis
*   **Amazon & Google Investments:**
    *   Amazon: $4.0B capital injection `[MEASURED]`.
    *   Google: $2.0B capital injection ($500M cash + $1.5B over time) `[MEASURED: Filings & Press Disclosures, Oct 2023]`.
*   **Circular Flow Quantification:** 
    *   Anthropic agreed to spend $4B+ over several years on AWS infrastructure (Trainium and EC2 compute) `[ASSERTED: Media reports / Company Announcements]`.
    *   A significant portion of capital raised from Big Tech investors flows directly back to their cloud divisions as compute lease payments.
    *   *Forensic Impact:* Revenue generated via AWS Bedrock (e.g., $550M) includes enterprise spending driven by AWS credits issued to startups and portfolio companies. An estimated **20%–30%** of Bedrock Claude consumption is financed via cloud-credit startup programs funded by AWS `[ESTIMATED]`.

#### E. Cash vs. Revenue & Unit Economics
*   **Inference Costs & Gross Margin:** Anthropic’s Claude 3.5 Sonnet exhibits superior developer unit economics due to optimized token efficiency. Gross margin on direct API usage is estimated at **50%–60%** `[ESTIMATED]`.
*   **Cash Burn Rate:** Anthropic burnt estimated **~$1.5B–$2.0B** in 2024, driven primarily by cluster reservation fees for AWS Trainium/NVIDIA H100 capacity and Anthropic 3.5/4 model training runs `[ESTIMATED]`.

#### F. Falsification Criteria
1.  **AWS SEC Filings / Segment Disclosures:** If AWS discloses Bedrock revenue contribution under 1% of AWS total revenue ($100B+ base), Anthropic's Bedrock run-rate claims would be contradicted. *(Result: AWS 10-Q filings report "AI services driving multi-billion dollar run-rates" across Bedrock, supporting the scale, though unsegmented).*
2.  **API Latency & Outage Log Reconstruction:** Analysis of third-party API monitoring logs (e.g., Datadog, Cloudflare) showing developer token drop-off. *(Result: Claude 3.5 Sonnet usage logged unprecedented growth in developer benchmarks from June–Nov 2024).*

---

### CASE FILE 3: xAI Corp.

#### A. Headline Claims vs. Definitional Forensics
*   **Headline Assertions:**
    *   $100M ARR achieved in late 2024 `[ASSERTED: Leaked investor pitch materials, Nov 2024]`.
    *   Targeting multi-billion dollar valuations on $5B–$6B equity rounds at $45B–$50B valuation `[ASSERTED: WSJ, Nov 2024]`.
*   **Definitional Forensic:** xAI’s consumer distribution is completely bundled with X Corp (formerly Twitter). Subscription revenue for "Grok" is derived from X Premium+ ($16/mo or $22/mo) subscriptions. There is **no independent standalone Grok consumer application subscription** operating at scale.

```
                     xAI Revenue Decomposition ($100M ARR)
  
  Total Run-Rate: ~$100M
  +-----------------------------------------------------------------------------------+
  | Intercompany Imputed Revenue from X Corp (Premium+) : ~$75M (75%) [ESTIMATED]     |
  | Grok Direct Enter
...[truncated for length]

---

**Claude:**

[⏰ 05:52, 22 сентября 2026]

---

> `Bash` -- {"command": "echo ok"}

---

**Claude:**

```json
{
 "lang": "mixed",
 "topic": "Форензика доходов frontier LLM-лабораторий: сходится ли подписочная и enterprise арифметика",
 "one_line": "Дипресёрч восстанавливает выручку OpenAI, Anthropic, xAI, Mistral, Perplexity и Cohere снизу вверх (подписки + enterprise) и проверяет, выдерживают ли headline-цифры проверку против аудированных якорей (Microsoft, Alphabet, Salesforce/Datadog/Snowflake).",
 "key_findings": [
  "Все шесть лабораторий частные и не подают аудированную отчётность — каждое 'ARR' есть либо самозаявление компании, либо утечка из инвесторской колоды, ни одно не GAAP-выручка; вся экосистема данных сводится к ~4 первичным источникам (The Information, Bloomberg, Ramp, Menlo Ventures), остальное — цитатное отмывание без независимого подтверждения",
  "OpenAI: заявленный run-rate '$40B' (авг.2026) — это аннуализация пикового месяца; реальный Q1 2026 = $5.7B выручки при burn $3.7B (65%); 'подписки $22B' на деле смешивают consumer Plus/Pro с B2B-местами; Pro-тир ($200) — лишь ~0.6% платящих пользователей (не 5.8%, как ошибочно растиражировано), что подтверждает H1 (тонкий срез дорогих тиров)",
  "Anthropic: наиболее концентрированный enterprise-кейс — Cursor+GitHub Copilot дают ~$1.2B из ~$4-5B (четверть выручки от двух клиентов), топ-1% клиентов = ~80% enterprise-выручки; хорошо обоснован уровень ~$5B, а рост до заявленных $30-65B за 11 месяцев не имеет первичного источника и оценивается как вероятная инфляция run-rate",
  "xAI — худший профиль качества выручки: AI-выручка ~$500M против burn ~$6.4B/год (сближается к аудированному через S-1 SpaceX, куда консолидировали xAI после слияния 02.2026), заявленные '$3.3B' смешивают легаси-рекламу Twitter/X с AI-выручкой",
  "Mistral честнее прочих: €1B к концу 2026 явно назван CEO 'целью', а не run-rate; текущий ARR ~€300-400M небольшой и правдоподобно enterprise-driven, хотя ASML одновременно инвестор и потенциальный клиент",
  "Perplexity: заявленный ARR $450M реконструируется лишь наполовину (~$240M подписок), остальное — аннуализация 50%-скачка за один месяц от нового продукта; структурно тонкая маржа, так как компания перепродаёт чужие модели (OpenAI/Anthropic/Google)",
  "Cohere: относительно чистый кейс — именные enterprise-клиенты (Oracle, RBC, Fujitsu), но между отчётами разброс $70M vs $240M ARR внутри года указывает на 'лоскутную' концентрацию сделок",
  "Калибровочные аудированные якоря показывают дисциплину, которой нет у частных лабораторий: Alphabet раскрывает $514B облачного RPO именно как backlog, а не выручку, и конвертирует лишь ~50% за 2 года; зрелым SaaS (Salesforce, Snowflake, Datadog) требуются ГОДЫ (5-15 лет) и 200-300 семизначных клиентов, чтобы дойти до $1B ARR — резкий контраст с месячными скачками у AI-лабораторий",
  "Итоговый вердикт: H1 (подписки не могут нести headline-выручку) подтверждён — дорогие тиры везде <1% платящих, блендовый ARPU ~$20-21; H2 (enterprise раздута концентрацией и определениями) подтверждена сильнее всего у Anthropic; H0 (цифры в целом реальны) частично подтверждена — спрос действительно беспрецедентен (burn и часть выручки реальны и болезненны), но лаборатории систематически подают run-rate как выручку, места как подписки, двух клиентов как рынок, пиковые месяцы как годы"
 ],
 "recommendations": [
  "Три числа, которые быстрее всего закрыли бы вопрос: (1) аудированная годовая GAAP-выручка OpenAI с разбивкой consumer/enterprise/API за вычетом сделок с Microsoft — появится только в S-1 при IPO; (2) выручка Anthropic за вычетом топ-10 клиентов (особенно Cursor и GitHub/Microsoft) — живёт в дата-руме инвесторов Anthropic; (3) отдельная AI-выручка и burn xAI без рекламы X — частично уже доступна в S-1/консолидированной отчётности SpaceX",
  "При использовании этих цифр в лабораторной документации об устойчивости рынка LLM-лабораторий: верить burn-показателям (болезненные и подтверждаемые), дисконтировать run-rate (переоценённая метрика), никогда не считать совпадение двух вторичных источников подтверждением, если оба восходят к одному первичному происхождению (Bloomberg/The Information/Ramp/Menlo)",
  "Разделять для каждой лаборатории 'реальная используемость' (аудировано или близко к тому: burn, часть API-объёма) от 'управленческая рамка' (run-rate, bookings, RPO, seat-бандлы) при построении витрины для рейза/acqui-hire анализа"
 ],
 "entities": {
  "people": ["Sam Altman", "Sundar Pichai"],
  "companies": ["OpenAI", "Anthropic", "xAI", "Mistral AI", "Perplexity", "Cohere", "Microsoft", "Alphabet", "Google Cloud", "Salesforce", "Datadog", "Snowflake", "Amazon", "AWS Bedrock", "Nvidia", "Oracle", "AMD", "SpaceX", "GitHub", "Cursor", "ASML", "Fujitsu", "RBC", "LG", "Notion", "Moderna", "PwC", "T-Mobile", "Morgan Stanley", "Amgen", "BNY Mellon", "Pfizer", "Bridgewater Associates", "Boston Consulting Group", "Asana", "GitLab", "Midjourney"],
  "products_tools": ["ChatGPT Plus/Pro/Team/Enterprise", "Claude.ai Pro/Max", "Claude Code", "GitHub Copilot", "Grok / SuperGrok", "Le Chat Enterprise", "M365 Copilot", "Google One AI Premium", "Gemini", "Vertex AI"]
 },
 "open_questions": [
  "Не найдены аудированные французские отчёты Mistral SAS (registre du commerce) — были бы источником правды по binding-контрактам vs pipeline",
  "Реальный gross margin после inference cost не раскрыт ни одной лабораторией (кроме грубых оценок 35-60%)",
  "Нет данных о разбивке доли выручки, приходящейся конкретно на related-party/инвестор-клиент циклы (Microsoft-OpenAI, Amazon/Google-Anthropic, ASML-Mistral, Nvidia-Cohere) в абсолютных цифрах",
  "Расхождение Cohere $70M vs $240M ARR в течение одного года не объяснено",
  "Насколько устойчива концентрация Anthropic на Cursor+Copilot при возможном развороте GitHub на модели Microsoft/OpenAI — не проверяемо на имеющихся данных",
  "Отчёт сгенерирован после обучающего среза моделей (январь 2026) — почти все цифры за 2026 получены live-поиском по некалиброванному вторичному рынку, вероятна дальнейшая ревизия"
 ],
 "related_concepts": ["run-rate-vs-gaap-revenue", "citation-laundering", "related-party-circular-deals-ai-labs", "enterprise-revenue-concentration-risk", "compute-for-equity", "ai-lab-ipo-s1-disclosure"]
}
```
