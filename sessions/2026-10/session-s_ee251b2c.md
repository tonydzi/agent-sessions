---
session: s_ee251b2c
date: 2026-10-08
words: 4407
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-08 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_ee251b2c` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-07-HUB-05-1558
REGISTRY TOPIC: LinkedIn: восстановление НАВСЕГДА забаненного за автоматизацию аккаунта (2018, [ВОЗРАСТ], 5 аккаунтов-уклонений) - каналы, GDPR Art.15/22, охват DSA, small claims (нога claudeai#bb (Fable 5.1 Max + Research), 27.6K, 17 источников, dr_leg_gate PASS; остальные 5 рельс розданы пирам (peer_help h-c045d2f6))

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


===== VENDOR: report (DR26-10-07-HUB-05-1558-linkedin-reinstatement-claudeai.md) =====
This is specific enough to go straight to research — no clarifying questions needed. I'll dig into the full case as you've framed it: documented precedents for permanent automation-ban reversals, the admit-vs-deny evidence, the ranked channel map, the GDPR Art.15/22 and DSA location-vs-citizenship questions, small claims, data export from a restricted account, and the irreversible mistakes. Starting now.

---


```
This block is not supported on your current device yet.
```


---

I've put together the report on getting dev-dev back. The odds are under 5%. I found no documented case of LinkedIn reversing a permanent automation ban the member admitted to. Of 2,106 EU appeals in LinkedIn's October 2023 report, 232 were granted, about 11%, and those were mostly content cases. The five accounts you opened afterwards make your case harder still.

**Don't click the reCAPTCHA yet.** The best first move is a GDPR data access request to LinkedIn Ireland's data protection officer, sent from your original Gmail. Unlike the appeal, you can send it more than once. Say clearly that it is not an appeal and not a request to delete anything. It should make LinkedIn tell you which violations are on your file, whether that's the 2018 automation alone or the later accounts too. It should also get you your 30,000 connections and your messages. If LinkedIn doesn't give a real answer, you can complain to the Irish regulator. In one published case from that regulator, LinkedIn re-reviewed a restriction, found one violation "not valid" and lifted the block.

Only after that should you use your single appeal, aimed at the specific decision LinkedIn names. It should be about 200 words:
- admit the 2018 automation;
- confirm all the tools are gone and commit to following the rules;
- add one sentence owning the later accounts and offering to have them closed.

**Other routes are mostly closed:**
- **EU Digital Services Act complaints:** these need you to be in the EU or have a registered address there, and a notice less than 12 months old. Your ban also came before the law applied.
- **Small claims court:** LinkedIn caps its liability at $1,000 and excludes "loss of data", and you broke the rule against bots.

**Mistakes you can't undo:**
- asking for anything to be deleted, which could wipe your connections;
- opening another account or using any automation tool;
- saying in the appeal that it was a mistake, when LinkedIn's logs show 1,442 invitations in one minute.

LinkedIn's site blocked direct access, so I'm quoting its pages from search-index copies dated 7 October 2026. The "one appeal per decision" rule comes only from third-party sites. The data protection form link and the CEO email address are unconfirmed, and I couldn't search Reddit or X directly.

---

<antArtifact identifier="compass_artifact_wf-s_9a3a2a2d_text/markdown" type="text/markdown" title="Reinstating a Permanently Banned LinkedIn Account: Odds, Ranked Channels and the One-Appeal Strategy" version_uuid="s_76fad707">
# Reinstating dev-dev: odds, ranked channels and the traps that cost the one appeal

**Verdict: the realistic chance of getting this exact account back is under 5% — call it 2–5%.** That estimate rests on four things:
- No documented reversal of an *admitted* permanent automation ban turned up anywhere.
- LinkedIn granted 232 of 2,106 EU appeals (about 11%) in its October 2023 DSA report. Those are mostly content appeals and almost all are cases where the member disputes the violation.
- Your violation is proven by LinkedIn's own logs.
- You opened five evasion accounts afterwards.

The one primary-source record of LinkedIn lifting a restriction after outside pressure (Irish DPC record no. 1242) worked only because LinkedIn found one of the violations "not valid". **Do not click the reCAPTCHA yet.** Your strongest first move is a GDPR Art. 15 / 15(1)(h) / 22(3) request to LinkedIn Ireland's DPO, sent from the original Gmail. It is not one-shot, it can force LinkedIn to name exactly which violations sit on the file (the 2018 automation alone, or the evasion accounts too), and it gives you a regulator route (the DPC) that has already led LinkedIn to re-review a restriction. Then spend the single appeal against the specific decision record it reveals.

Labels used throughout: **VERIFIED** = primary source (LinkedIn page text from the live search index on 7 Oct 2026, EU or regulator document); **REPORTED** = someone's account; **INFERENCE** = mine. LinkedIn.com blocked direct fetching, so LinkedIn page wording is the indexed text as of 7 Oct 2026, not a rendered page.

## TL;DR
- **Odds are low single digits.** No admitted permanent automation ban has a documented reversal. The documented "permanent" reversals involved people who denied wrongdoing, notices that were really temporary, or a regulator-forced re-review that found a violation invalid.
- **Strongest first move:** a GDPR Art. 15 + 15(1)(h) + 22(3) request to the LinkedIn Ireland DPO from the original Gmail. Explicitly say it is **not** an appeal and **not** an erasure request. It gets you the named reason, the account-status history, the linked-account findings and your full connections/messages export. Spend the one appeal only after that, with an admit-and-commit text that also briefly owns the evasion accounts.
- **The DSA lane is effectively closed and small claims is weak.** For the DSA, User Rights needs an EU location or registered address and a notification less than 12 months old, and your ban predates the DSA. For small claims, there is a $1,000 liability cap that excludes "loss of data", and you breached the bot clause. The irreversible mistakes are any erasure request, any new account or automation, and burning the appeal on "it was a mistake".

## Key Findings

### Q1. Base rates and precedents
- **None found for your shape of case.** I and a dedicated sub-search found **no first-person record of a permanent automation or mass-invitation ban being reversed after the member admitted it** (REPORTED, null result). Reddit, X and Trustpilot could not be searched directly, so threads may exist that I could not see.
- **Documented "permanent" reversals don't match your facts:**
  - **Blake Harber (Substack, May 2023)** got a "permanently restricted" notice repeated five times in 12 hours. It was lifted about 40 hours later after influential contacts escalated (he names Chris Orlob, Mike Molinet and Scott Leese). He denied wrongdoing and the reason was not stated (REPORTED). He had also opened a new account, which LinkedIn noticed and treated as personal ban evasion — the closest thing to an evasion precedent, but not an admitted-automation case.
  - **Melanie Goodman (LinkedIn consultant, Substack, Sept 2025)** sent about 30 tickets with no result. Her account was restored "within hours" of a lawyer-style letter citing DSA Arts. 14/17/20/21/23, after she also emailed the CEO. Support had told her "about 15 x" that the account was permanently closed, but it was formally a 10-week *temporary* restriction, and LinkedIn "admitted fault" (REPORTED). She had EU standing and a non-violation case.
  - **Sachin Sharma (Substack):** a [ВОЗРАСТ] account was permanently restricted, "multiple appeals" failed, and LinkedIn "refused to clarify quoting their privacy policy". His replacement account was later restricted too (REPORTED). This is the typical outcome, and it is what happened to your five accounts.
  - **Hedley Rees (Substack):** permanently removed in 2021 for misinformation. He came back only by registering a new account with a different email (REPORTED). That is not a reinstatement, and it is excluded for you.
- **Regulator-driven reversals are real but aimed at deletion.** In **Irish DPC record no. 1242 (dated 27 March 2024)** the member made an Art. 15 access request and an Art. 17 erasure request on 21 Dec 2022. LinkedIn refused because the account "had been restricted, due to violations of the Respondent's License Agreement". After a complaint to Italy's Garante, transferred to the DPC on 18 July 2023, LinkedIn "reviewed the Data Subject's restriction and determined that one of the violations that led to the account being restricted was not valid and it removed the block from the account". It then deleted the account and admitted the access request was "initially overlooked" through "human error". Total time was about 9 months (VERIFIED: https://www.edpb.europa.eu/system/files/2024-10/decision-no-1242.pdf). The sub-search reported two similar DPC records where restrictions were lifted to allow deletion or access (REPORTED; I did not fetch them myself): https://www.edpb.europa.eu/system/files/2024-06/ie-2022-12-decisionpublic_redacted_0.pdf and https://www.edpb.europa.eu/system/files/2024-06/ie-2023-02-decisionpublic_redacted.pdf.
- **LinkedIn's EU appeal statistics.** The October 2023 LinkedIn DSA transparency report shows 2,106 appeals, 232 granted, a median of **49 minutes** from appeal to decision, and 2,047 "permanent account suspensions due to repeatedly providing policy-violating content" (VERIFIED: https://content.linkedin.com/content/dam/help/linkedin/en-us/October-2023-LinkedIn-DSA-Transparency-Report.csv). INFERENCE: a 49-minute median means most appeals are triaged against a playbook, not re-investigated, so your text has to fit a reinstatement path the reviewer already has.
- **Plainly:** for an admitted permanent automation ban with later evasion, the evidence says reversal is rare enough that no one has documented it. Treat reinstatement as a long shot and the contact data (Q7) as the realistic win.

### Q2. Does admitting it help or hurt?
- **LinkedIn's own policy names agreeing to comply as the reinstatement path:** "Repeated violations may result in account restriction. We provide the opportunity to appeal an account restriction, and we may reinstate a restricted account if the member agrees to comply with these Professional Community Policies." (VERIFIED: https://www.linkedin.com/help/linkedin/answer/a1342754). The same sentence appears in LinkedIn's H2 2024 Terms of Service report to the California Attorney General (VERIFIED: https://oag.ca.gov/sites/default/files/LinkedIn%20California%20Terms%20of%20Service%20Report%20--%20H2%202024.pdf/LinkedIn%20California%20Terms%20of%20Service%20Report%20--%20H2%202024.pdf).
- **LinkedIn's support template uses the same formula.** In a 2021 case reply quoted by Hedley Rees: "You may appeal the restriction by responding to this email with your agreement and intent to comply with our User Agreement and our Professional Community Policies." (REPORTED). The reply listed each violating item with a timestamp, so specific reasons do exist on file.
- **The automation page frames compliance as the way back for automation suspensions:** "Review and disable the software or extension that automates activities. Your account will then automatically be re-enabled at the time specified on the suspension notification." (VERIFIED: https://www.linkedin.com/help/linkedin/answer/a1340567). That covers time-limited suspensions. Nothing in the policies promises the same for permanent ones.
- **"It was a mistake" is the worst option for you** (INFERENCE). Your file shows 1,442 invitations in one minute. A denial contradicts logs the reviewer can see and destroys the credibility of any commitment.
- **Silence about the evasion accounts — INFERENCE, no evidence either way.** I found **no policy text or ex-employee account** on whether volunteering evasion helps. LinkedIn already links them, since each died at identity verification and Harber's new account was spotted. Our position: acknowledge them in one sentence, near the end, as a mistake you understand was itself a violation, and offer to have them closed. Do not lead with them or describe them. Hiding a fact the reviewer can see makes the "I will comply" pledge worthless.
- **No ex-Trust & Safety insider sources found.** I could not find any ex-LinkedIn T&S blog or interview on how admissions are treated.

### Q3. Channel map, ranked by observed success for this shape of case
1. **GDPR Art. 15/15(1)(h)/22(3) request to the LinkedIn Ireland DPO.** **Do this first.**
   - Address: the DPO web form `https://www.linkedin.com/help/linkedin/ask/TSO-DPO` (REPORTED by a third-party privacy notice and a Microsoft Q&A thread; it may work without signing in; not confirmed live). LinkedIn's GDPR page says only "To learn more about our DPO and how to contact them, please see our Privacy Policy" (VERIFIED: https://privacy.linkedin.com/gdpr). Postal backup: LinkedIn Ireland Unlimited Company, Wilton Place, Dublin 2 (REPORTED by request-gdpr.com).
   - Who reads it: privacy operations (INFERENCE).
   - Timing: one month, extendable by two (GDPR Art. 12(3)).
   - Not one-shot.
   - Outcomes: one primary-source case (DPC 1242) where the follow-up DPC complaint produced a re-review of the restriction. A Microsoft Q&A commenter said of the DPO form "They never helped" (REPORTED).
2. **The single Help Center / on-screen appeal** (your drafted form).
   - The one-appeal rule: "You may appeal each decision only once" is REPORTED as the text of LinkedIn's redress-rights page by awarexone.com and linkedapi.io. I **could not retrieve the LinkedIn page itself or its URL**, so I have no primary text on whether later submissions are ignored or merged.
   - The account-restrictions page tells content-restricted members to "login and follow the onscreen prompts to ask us to revisit our decision" (VERIFIED: https://www.linkedin.com/help/linkedin/answer/a1340522).
   - The "second look" contact form for automation restrictions requires login and "is being gradually rolled out and is currently available only to some LinkedIn members" (VERIFIED: a1340567).
   - Median decision time for EU appeals: 49 minutes (VERIFIED, 2023 report).
3. **Complaint to the Irish DPC** via forms.dataprotection.ie, if the DPO stonewalls or sends only boilerplate. Timeline from the precedent: about 9 months. Outcome: restriction re-reviewed (VERIFIED, record 1242).
4. **Executive email.** `[EMAIL]` is REPORTED by Melanie Goodman as getting her case "flagged, escalated, and resolved". The address pattern is unverified. That success came on a temporary, wrongful restriction.
5. **@LinkedInHelp on X.** REPORTED by Goodman as the "quickest route" to getting a ticket opened. No documented outcome for a permanent automation ban.
6. **Letter to LinkedIn's outside counsel.** REPORTED by Goodman as getting a response "within hours", but backed by DSA standing and a non-violation case. Without either, it is just a threat letter (INFERENCE).
7. **DSA Art. 20/21 (User Rights GmbH).** Effectively closed — see Q5.
8. **No evidence found** for the `/help/linkedin/ask/ppq` form, Premium live chat (INFERENCE: you can't buy or use Premium on an account you can't log into, so it isn't a lever), Microsoft CELA or other Microsoft corporate escalation, the BBB (Sunnyvale), the FTC or the California AG. INFERENCE: the FTC and the AG don't resolve individual account disputes. The AG's link to LinkedIn is the ToS transparency report above, not individual redress. Treat all of these as unproven, and don't use them before the DPO request.
9. **Going to an in-person LinkedIn office before filing any ticket** is REPORTED by Goodman as fastest. That claim is anecdotal.

### Q4. GDPR as a crowbar
- **What the law now requires.** In *CK v Dun & Bradstreet Austria* (C-203/22, 27 Feb 2025), the CJEU held that Art. 15(1)(h) is "a right to an explanation of the procedure and principles actually applied in order to use, by automated means, the personal data of the data subject with a view to obtaining a specific result" (para. 58). A complex formula or step-by-step description is not enough (para. 59). If the controller claims trade secrets, it must give the information to the supervisory authority or court, which decides the balance (VERIFIED: https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX%3A62022CA0203).
- **Does Art. 22 reach account bans?**
  - **For you:** the Amsterdam Court of Appeal (4 Apr 2023; ECLI:NL:GHAMS:2023:793/796/804) held that Uber's deactivation of drivers was solely automated. It found the human review "not… much more than a purely symbolic act" and ordered explanations (VERIFIED as reported by Fountain Court Chambers and Fieldfisher).
  - **Against you:** LinkedIn tells EU regulators that its automation enforcement includes "Conducting manual investigation and restriction of accounts engaged in automated activity" (VERIFIED: LinkedIn's September 2025 Code of Practice on Disinformation report, https://disinfocode.eu/reports/microsoft-linkedin/6/text). Expect LinkedIn to argue the decision was not "solely automated" (INFERENCE).
  - **Use Art. 22 as a question, not an assertion.** Ask whether the decision was solely automated and, if humans were involved, what they actually reviewed. Either answer helps you.
  - In *SCHUFA* (C-634/21, 7 December 2023), the CJEU held that an automated credit score is itself "automated individual decision-making" under Art. 22(1) "where a third party… draws strongly on that probability value" (as summarised by the Library of Congress Global Legal Monitor, 10 Jan 2024; Bird & Bird: "the concept of decision is broad and includes acts that may affect the individual in various ways").
- **Precedent specific to LinkedIn:** DPC 1242 (above) is the only one found. noyb has a pending complaint before the Austrian DPA saying LinkedIn withholds profile-visitor data from Art. 15 responses (VERIFIED as noyb's own claim: https://noyb.eu/en/linkedin-locks-your-gdpr-rights-behind-paywall). Expect partial answers and plan to escalate.
- **Wording that gets a substantive answer** (INFERENCE, built on the above):
  - Name the controller (LinkedIn Ireland UC).
  - Cite Arts. 15(1), 15(1)(h), 15(3), 22(3) and C-203/22 para. 58.
  - List the exact data categories you want. LinkedIn's own export schema includes "Account Status History… the date and time the member's account was created, closed, reopened, or restricted" and "Inferences", and it says data outside the files can be requested through its "Data Access Request Form" (VERIFIED: https://www.linkedin.com/help/linkedin/answer/a1339364/downloading-your-account-data).
  - State: "This is not an appeal of any restriction decision and not a request for erasure; do not close or delete the account."
  - Ask for each violation record behind each restriction, the policy clause applied, whether any decision was solely automated, and any determination linking other accounts to you.
- **Jurisdiction trap** (INFERENCE): the User Agreement's contracting party now follows your residence. Since you now live in the US, LinkedIn may answer as LinkedIn Corporation or say GDPR doesn't apply. Rebut this by pointing out that the restriction and the processing were done by LinkedIn Ireland while you were EU-resident (GDPR Art. 3(1)).
- **Does a named reason hurt the later appeal?** No evidence either way. INFERENCE: it helps, because the reason is already on file. Knowing whether the evasion accounts are recorded as separate violations decides how you write the one appeal. DPC 1242 shows a restriction can rest on several recorded violations, some of which may be invalid.

### Q5. The DSA lane without an EU address
- **The regulation follows location, not citizenship.** Art. 2(1) applies to "recipients of the service that have their place of establishment or are located in the Union" (VERIFIED, Regulation (EU) 2022/2065). The DSA Observatory reads "located" as not requiring legal residence, so temporary physical presence may count (REPORTED, academic commentary). It notes that DSA complaints to regulators under Art. 53 are limited to recipients located or established in a Member State. A Polish passport alone does not qualify you.
- **User Rights' rules close it twice:**
  - "We can only process complaints from users who are located in, or have a registered address within, the European Union."
  - "We cannot process your complaint if you received the notification from the platform more than twelve months ago."
  - (VERIFIED: https://www.user-rights.org/en/faq). It does cover LinkedIn and is free to users.
- **The ban also predates the DSA** (INFERENCE). The DSA has applied to all platforms since 17 Feb 2024, so no Art. 17 statement of reasons was owed for a 2021–22 decision. A *new* rejection of your appeal issued in 2026 could arguably be a fresh decision, but only if you are "located" in the EU at that point.
- **On meldunek:** I found **no published list of residence documents** that User Rights accepts. A Polish registered address would probably satisfy the "registered address" limb (INFERENCE). Don't obtain one just for this unless you genuinely live there.
- **Appeals Centre Europe** (Dublin) does not cover LinkedIn. Its own "Our Work" page (appealscentre.eu/our-work, modified 5 Aug 2026) lists only "Facebook, TikTok, Instagram, YouTube, Pinterest, Threads, Google Maps" and says "If a platform or policy isn't listed, it means we just do not cover it yet." It began hearing account-suspension disputes on 6 June 2025 (RTÉ), and RTÉ reports users are currently not charged, with the €5 fee described as a future fee.

### Q6. Small claims / legal
- **Forum, verified:** for non-EU users, "all claims and disputes can be litigated only in the federal or state courts in Santa Clara County, California, USA". Designated-Country residents get the courts of their country of habitual residence, or Ireland. Section 6 adds: "You may have additional rights of redress and appeal for some decisions made by LinkedIn that impact you." (VERIFIED: https://www.linkedin.com/legal/user-agreement, indexed text).
- **Arbitration:** none appears in the indexed User Agreement text. LinkedIn's *Ads Agreement* and *LMS Program Terms* do contain binding arbitration with a small-claims carve-out (VERIFIED: https://www.linkedin.com/legal/sas-terms). One summary site (TermsDecoded) wrongly describes the User Agreement as having "mandatory arbitration limited to California courts". Treat "no arbitration" as likely but not fully verified, because I couldn't render the full page.
- **Liability cap:** liability is capped at "(A) THE TOTAL FEES PAID OR PAYABLE BY YOU… OR (B) US $1000". Excluded damages include "LOSS OF DATA" (VERIFIED, indexed User Agreement).
- **Precedents and theory of harm:** I found no documented small-claims suit over a LinkedIn account closure. Your theory of harm is weak (INFERENCE): the service is free, and the User Agreement bars bots used to "add or download contacts, send or redirect messages", which is what you admit doing. A demand letter has only REPORTED effect, and only where the member had a non-violation case and DSA rights. The California Courts Self-Help Guide (selfhelp.courts.ca.gov/small-claims-california) says "Generally, you can only sue for up to $12,500 in small claims court (or up to $6,250 if you're a business)", with filing fees of "$30-$100", no lawyer representation ("You can't have a lawyer represent you"), and "If you started the case, you can't appeal if you lose your case." I did not verify what non-money relief those courts can order.

### Q7. The contacts, separately from the account
- **Self-service export won't work while restricted** (INFERENCE from the help page). It needs a login via Settings & Privacy, and the sub-search found a LinkedIn support reply (quoted on a third-party blog) saying "Once the account is restored, you can download your account data history" (REPORTED).
- **The Art. 15 route does work for restricted accounts.** In DPC 1242 the restricted member eventually got "a copy of all their data" (VERIFIED). Ask in the same DPO request for Connections, messages, InMail and invitations, plus Art. 20 portability in machine-readable form. The Ola ruling held that PDF output is not "structured, commonly used and machine-readable" (VERIFIED as reported by Gigpedia).
- **CCPA right-to-know to LinkedIn Corporation as a parallel request:** I did not research this. INFERENCE: it is plausible as a backup if LinkedIn Ireland disclaims the account.
- **Limit:** LinkedIn gives "only… your own personal data and not that of other members" (VERIFIED, a1339364). Connection email addresses appear only where the connection allowed it (INFERENCE).

### Q8. What you'd regret not knowing, and the irreversible mistakes
- **Never ask for erasure (Art. 17), not even of the evasion accounts in loose wording.** In the DPC precedents, LinkedIn lifted restrictions *so that it could delete the account*. Deleting 30,000 connections cannot be undone.
- **Don't spend the one appeal before you know what's on the file.** If the record shows separate violations (2018 automation plus each evasion account), an appeal that addresses only 2018 is wasted. The DPC case shows that individual violations can be struck down.
- **Every new account, automation tool, VPN or third-party "recovery service"** is read as further evasion. Sharma's replacement account and your five accounts show how that ends.
- **Don't deny what the logs show.** "Third-party tool, not me" or "it was a mistake" will be checked against the 1,442 invitations in one minute.
- **Use only the original Gmail and the original profile URL**, and quote the case or reference number. A submission from another identity proves the linkage they are already worried about.
- **Don't go legal first.** Threats before the DPO request may move the file to the legal team and freeze ordinary T&S review. That is INFERENCE; no evidence either way.

## Recommendations (in order)
1. **Leave the reCAPTCHA unclicked.** Within 7 days, send the DPO request through the TSO-DPO form from the original Gmail, and send the same text by post to Wilton Place, Dublin 2. Include:
   - Art. 15(1) full copy;
   - Account Status History;
   - every violation record and policy clause behind each restriction;
   - any linked-account determinations;
   - Art. 15(1)(h)/C-203/22 explanation of the logic, and whether the decision was solely automated (Art. 22(3));
   - connections, messages, InMail and invitations in machine-readable form (Art. 20);
   - the express sentence: "This is not an appeal of any restriction decision and not a request for erasure."
2. **Day 31 with no substantive answer** (or day 90 if LinkedIn extends): complain to the DPC, attaching DPC record 1242 as the precedent.
3. **Then submit the one appeal**, citing the exact decision. Use the a1342754 sentence. Admit the 2018 automation specifically. Confirm all tools are gone. Make a concrete compliance commitment. Add one sentence acknowledging the later accounts as a violation you won't repeat, with an offer to have them closed. Keep it to about 200 words.
4. **Only if that is rejected:** the CEO email and @LinkedInHelp. Expect little.

## Caveats
- I could not fetch LinkedIn.com pages directly. All LinkedIn wording is the indexed text as of 7 Oct 2026, and the "appeal each decision only once" page is quoted only secondhand.
- Reddit, X, Trustpilot, the BBB and court dockets could not be searched directly, so the null result on precedents is strong but not exhaustive.
- The DPO form URL, the CEO email and the outside-counsel route are REPORTED and not confirmed live.
- The probability figure is my judgement from the evidence above, not a measured rate.
</antArtifact>


REMINDER: output ONLY the JSON object, nothing else.

---

**Claude:**

You've hit your weekly limit · resets Oct 10, 4am (Europe/London)
