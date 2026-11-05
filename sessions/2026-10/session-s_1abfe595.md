---
session: s_1abfe595
date: 2026-10-26
words: 3347
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-26 · You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_1abfe595` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

You are distilling a DEEP-RESEARCH report into a compact, searchable knowledge note.
One report, possibly assembled from several AI vendors researching the SAME question.

DR-ID: DR26-10-25-HUB-01
REGISTRY TOPIC: Acute Rhinitis (Runny Nose & Sneezing): Summary of Evidence and Self-C

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


===== VENDOR: report (DR26-10-25-HUB-01-acute-rhinitis-runny-nose-sneezing-summary-of.md) =====
# Acute Rhinitis (Runny Nose & Sneezing): Summary of Evidence and Self-Care

**Executive Summary:**  An acute onset of heavy sneezing, watery rhinorrhea and nasal congestion (no sore throat) suggests allergic or viral rhinitis (or irritant rhinitis).  We found **limited evidence** for any natural remedy giving rapid (24–48 h) relief.  The safest measures with some support are **adequate hydration and nasal saline irrigation** (flushing mucus).  Zinc lozenges (≈75 mg/day) started within 24 h may shorten a cold by ~2 days, but evidence is low-quality and causes nausea.  Honey (a teaspoon) can soothe cough and sore throat.  Other popular remedies (garlic, echinacea, vitamin C, homeopathy, essential oils, etc.) lack credible RCT evidence for acute benefit.  Standard allergy treatments (antihistamines, nasal steroids) are effective but take hours–days and are not “instant cures.”  If symptoms worsen (high fever, severe pain, long duration), seek medical care.

## Differential Diagnosis

| Feature           | Allergic Rhinitis                   | Viral (Common Cold)                                      | Nonallergic/ Irritant Rhinitis                   |
|-------------------|-------------------------------------|----------------------------------------------------------|-------------------------------------------------|
| **Onset**         | Often sudden on allergen exposure, may be seasonal or perennial (pets, pollen). <br>Many exposures necessary for symptoms.  | Gradual over 1–3 days after incubation (e.g. rhinovirus). | May be sudden (upon exposure to irritant) or gradual; often persistent or triggered by weather/odor. |
| **Symptoms**      | Sneezing, clear runny nose, congestion, **itchy** eyes/nose/throat, watery eyes, may cough. <br>No fever.  | Sneezing, clear to mucoid discharge, congestion, cough, chills, mild fatigue, sometimes low-grade fever (≤38°C). <br>Post-nasal drip, mild malaise. | Sneezing or congestion without allergy (no itch, no allergen). <br>Symptoms often non-itchy, with rhinorrhea or congestion triggered by irritant exposure. <br>Often no systemic symptoms. |
| **Course**        | May last days-weeks if allergen exposure persists.  | Self-limited ~5–10 days; peak around day 2–3. Usually no return of fever once cold established. | Chronic or recurrent as long as irritant persists; typically not associated with infectious course unless virus is trigger. |
| **Triggers/History** | Seasonal patterns; known allergies; family history of allergies/asthma.   | Exposure to infected contacts; common in cold seasons.  | Exposure to smoke, fumes, perfumes, cold air, spicy food, etc..  No IgE sensitization. |
| **Physical exam / Tests** | Pale/blue nasal mucosa (swollen turbinates), clear discharge. Skin or serum IgE tests confirm allergens. Nasal smear: eosinophils (often). <br>Normal vitals, no fever. | Red, swollen nasal mucosa; clear to yellow discharge over time. Viral culture/PCR rarely needed. No allergen IgE.  Mild fever possible.  | Nasal mucosa often normal or erythematous. No allergen IgE. No systemic signs.  Provocation with irritant elicits symptoms. |
| **Key distinctions** | Itchy eyes/nose, allergies present, no fever. Improves with antihistamines. | May have systemic symptoms (malaise, mild fever), cough.  Colds often start with sore throat or fever (though patient here reports none). | Symptoms closely tied to irritant exposure; lacks itch and IgE markers.  Often in adults >20y. |
| **Red flags (urgent)** | Unilateral symptoms, severe pain, high fever, or purulent discharge suggests sinusitis or other cause.  | High fever (>3d), severe headache/facial pain, ear pain (otitis), wheezing/Dyspnea.  Consider flu/COVID if risk/exposure. | New asymmetry, visual changes, or neurological signs. |

## Evidence Matrix of Natural Remedies

| Intervention                   | Acute Symptom Relief (≤48h)                   | Shortened Illness Duration   | Prevention (cold incidence)    | Chronic Allergy Use (weeks)                 | Notes / Safety (confidence)                                      |
|--------------------------------|-----------------------------------------------|------------------------------|---------------------------------|---------------------------------------------|------------------------------------------------------------------|
| **Hydration (fluid intake)**   | No RCTs show “extra” water beyond normal helps more; but **adequate hydration** is advised to keep mucosa moist.  | N/A (supportive care)         | N/A                             | N/A                                         | Avoid dehydration; no risk if moderate. [established]           |
| **Warm drinks/tea**            | Small RCT (n=30) showed hot drink gave *subjective* relief of symptoms, but no objective airflow improvement. Anecdotal comfort.  | –                            | –                               | –                                           | Very limited evidence [speculative]. Safe.                        |
| **Honey (alone or in warm milk)** | Evidence (mostly pediatric): a spoonful of honey may soothe cough/throat better than no treatment. May temporarily relieve cough/sore throat (not proven for congestion).  | –                            | –                               | –                                           | Do **not** give to infants <1y (botulism risk). [emerging] |
| **Milk (mucus myth)**          | No evidence that milk increases nasal mucus or worsens congestion. The “milk causes mucus” belief is a myth (no clinical support).  | –                            | –                               | –                                           | Safe generally; choose alternatives if patient dislikes it. [speculative] |
| **Garlic/onion**               | No RCT shows benefit for acute symptoms.  A single RCT (n=146, 12-week prophylaxis) showed fewer colds with daily garlic supplements, but **no evidence for immediate relief**.  | No effect on cold duration shown.    | Possibly reduces incidence (one small trial) | –                             | Raw garlic/orion in nose or mouth can irritate. Risk: bleeding if applied. [speculative] |
| **Fermented foods / probiotics** | No acute URTI RCT demonstrating quick relief. Some meta-analyses suggest daily probiotics slightly reduce URTI incidence/duration in kids, but heterogeneity high.  | Modest (1–2 days) reduction in duration in some trials; evidence low. | Slight decrease in cold frequency (unproven) | Some studies for eczema (allergy) only. | Generally safe (if non-immunocomp); possible bloating. [emerging] |
| **Turmeric/curcumin**         | No evidence in acute cold.  One RCT (n=241, 2-month pollen season) found curcumin improved allergic rhinitis symptoms vs placebo – irrelevant to acute URTI.  | –                            | –                               | May help chronic allergic inflammation (low-quality data). | Safe at culinary doses; high-dose long-term needs caution (bleeding risk). [speculative] |
| **Ginger**                     | No RCT for acute cold relief. Folk remedy for nausea/anti-inflammatory.  | –                            | –                               | –                                           | Safe as tea/spice. [speculative]                                 |
| **Chamomile**                  | No evidence in colds.  A tea is soothing (placebo). Chamomile allergy possible.  | –                            | –                               | –                                           | Generally safe (flower tea); caution in ragweed-allergic. [speculative] |
| **Echinacea**                 | Multiple RCTs & meta-analyses show **no consistent benefit** for treating or preventing colds.  | –                            | –                               | Some studies in allergic rhinitis show no clear benefit. | Safe short-term; possible allergic reactions. [low-certainty]   |
| **Elderberry (Sambucus)**      | A few small RCTs (flu infections) suggest elderberry syrup may **mildly reduce cold/flu symptoms** (e.g. 4 days faster in one study), but evidence is preliminary. Short-term benefit uncertain. | –                            | –                               | –                                           | Raw berries are toxic. Generally safe cooked syrup up to 2 weeks. [emerging] |
| **Andrographis (Kan Jang)**    | Some RCTs (often in Europe/India) report faster symptom relief in colds vs placebo. Meta-analyses suggest modest reduction in symptom scores and duration (pooled ~1 day shorter).  | ~1 day reduction (low-quality) | –                               | –                                           | Bitter taste; mild GI upset. [emerging]                         |
| **Pelargonium sidoides (EPs 7630)** | Cochrane review: may relieve symptoms of acute rhinosinusitis and common cold in adults, but evidence is **very low quality**. One trial showed improvement by day 10 but not day 5.  | Possibly reduces severity by ~day 10 (not 48h) | –          | –                                           | Some GI upset; caution in allergy to geranium family. [emerging/low-certainty] |
| **Nigella sativa (black seed)** | No human trials for acute cold. A few small studies suggest some benefit in allergic rhinitis (improved nasal symptoms over weeks) – no acute data. | –                            | –                               | –                                           | Generally safe (nut allergy possible). [speculative]            |
| **Butterbur (PA-free)**        | No evidence for cold. Studies (leaf extract) show improvement of hay fever symptoms over weeks.  | –                            | –                               | May relieve allergic rhinitis symptoms (as effective as antihistamines in some trials). | **Hepatotoxicity risk:** only use certified PA-free products. Not for acute use. [emerging] |
| **Homeopathy**                 | Numerous trials: *no evidence* of efficacy for colds or any condition beyond placebo.  | –                            | –                               | –                                           | Generally safe due to dilution; but possible delays in effective treatment. [fringe] |
| **Steam inhalation / humidifier** | Steam or warm mist may provide temporary comfort (humidity soothes mucosa). One RCT showed hot drinks (steam) improved subjective symptoms but not objective airflow. Warm, humid air can ease congestion.  | –                            | –                               | –                                           | *Safety:* avoid scalding burn from hot steam. Use warm (not boiling) steam or humidifier. [emerging] |
| **Essential oils** (menthol, eucalyptus) | E.g. menthol chest rub or steam: at best they give a cooling sensation and subjective relief of congestion. No RCT evidence for actual symptom reduction.  | –                            | –                               | –                                           | Avoid in nose/mouth (irritation). Diffusing oils at low dilution is safer. [fringe] |
| **Nasal saline (sprays or irrigation)** | Clears mucus, moistens passages. RCTs suggest saline irrigation provides symptom relief in colds/sinusitis (flushes pathogens, reduces congestion).  Often recommended as first-line symptomatic relief.  | May slightly reduce symptom duration via prevention of secondary infection (long-term use one trial showed fewer “illness days” over months, but not acute effect).  | –                               | Adjunct in allergic rhinitis (loosen secretions). | Very safe if using **distilled/boiled water**. Avoid force in severely blocked nose. [established] |
| **Oral Zinc (lozenges)**       | Start ≤24h from onset: meta-analyses show zinc (lozenges, ≥75 mg/day) may shorten cold duration by ~2 days (MD -2.37 d; CI -4.21 to -0.53).  It may also modestly reduce symptom severity.  | As above: ≈2 days shorter (duration). | No effect on preventing colds.  | –                                           | *Adverse:* nausea, taste disturbance, GI upset. **Do not use intranasal zinc** (FDA warning for permanent anosmia). Limit long-term dose (<40 mg/day) to avoid copper deficiency. [emerging/low-certainty] |
| **Vitamin C**                  | Meta-analyses (Hemilä et al): routine high-dose vitamin C (≥200 mg daily) shortens colds by ~8% (≈0.5 day) in prophylactic use; starting it *after* onset has minimal effect. | Slight (~1 day) reduction if taken daily, but effects small. | No effect on incidence in general population (except minor benefit in extreme physical stress). | –                                           | Doses up to ~2g/day short-term are safe; GI upset at high dose. [established (for prevention)] |

## Prioritized 0–48 h Self-Care Plan

1. **Hydration & Rest:** Drink fluids (water, herbal tea) to keep mucous membranes moist. Avoid dehydrating beverages (excess alcohol/coffee). Rest and sleep well.  
2. **Nasal Saline Irrigation:** Use isotonic saline spray or neti pot 1–2×/day. This rinses mucus and irritants.  Use sterile/distilled/boiled (cooled) water.  This often provides immediate congestion relief.  
3. **Zinc Lozenges:** If started within 24 h of symptoms, try zinc gluconate lozenges (≈13–23 mg each, total ~75 mg/day).  It may modestly reduce illness duration.  *Do not use intranasal zinc* (risk of anosmia). Stop if bad taste or nausea occurs.  
4. **Warm Fluids and Steam:** Sip warm herbal tea or broth; inhaling warm (not scalding) steam from a shower or bowl can soothe nasal passages. Evidence for cold cure is weak, but these measures improve comfort. Be careful to avoid burns.  
5. **Honey for Cough/Throat:** If cough or throat irritation is present, take 1–2 teaspoons of honey (alone or in warm tea) as needed. Studies (mostly in children) show it soothes coughs as well as OTC meds.  (Never give honey to infants <1y.)  
6. **Symptomatic Aids (optional):** Menthol rub or lozenges may give a cooling sensation; saline nasal drops/spray can relieve dryness (spray gently).  Chamomile or ginger tea is soothing (though no evidence of antiviral effect).  
7. **Monitor & Limit Remedies:** Do **not** overconsume any supplement. Avoid unproven intranasal remedies (garlic, onions in nose, essential oils) to prevent irritation.  
8. **Assess and Wait:** Most colds improve in ~5–7 days. If no improvement in 7–10 days or if symptoms worsen (see **Urgent Signs**), see a clinician.

## Unproven Claims & Evidence Gaps

- **False “Cures”:** Claims of a “1–2 day cure” lack evidence. No treatment reliably eradicates a cold in 1–2 days. Studies measure duration in days or symptom scores, not immediate cure.  
- **Garlic/Cabbage/Onion:** Anecdotal only. One small trial suggested garlic supplements might reduce cold incidence, but no evidence for rapid relief or treatment of established cold.  
- **Fermented Foods/Probiotics:** General immune-boosting claims have weak support. RCTs on probiotics show modest URTI reduction at best, but preparations vary widely. No data on immediate symptom relief. Well-controlled trials are needed.  
- **Herbs (Turmeric, Ginger, Echinacea, etc.):** Current RCTs for these focus on chronic allergy or prophylaxis, not acute colds. For example, curcumin helped allergic rhinitis over months, but no cold trials. Echinacea reviews show no consistent benefit. High variability in herbal extracts limits conclusions.  
- **Homeopathy:** Extensive reviews (e.g. Cochrane, NCCIH) conclude homeopathic remedies perform no better than placebo. Any perceived effect is likely placebo.  
- **Steam/Oils:** No RCT shows major benefit of steam inhalation or essential oils for colds. They provide comfort only. Repeated inhalation of very hot steam *can* cause burns. Menthol/eucalyptus rubs feel refreshing but do not change disease course.  
- **Vitamin C for Treatment:** Taking vitamin C *after* symptoms start has not shown significant benefit. Its effect is mainly prophylactic (if taken daily) and is small. Extra high-dose vitamin C does not guarantee quick relief.  
- **Hydration Beyond Adequate:** No study finds that “drinking extra” cures a cold faster beyond simply preventing dehydration. 

*Key evidence gaps:*  Most herbal remedies lack large, high-quality RCTs for acute use. Placebo-controlled trials measuring 24–48h symptom scores would clarify any rapid-acting effects.  Standardizing doses and preparations is also needed.  Until then, claims of rapid cure remain unsupported.

## Urgent/Care-Seeing Signs

Seek medical care if any of the following occur:

- **Severe or Prolonged Fever**: High fever (>38.5 °C) persisting >3 days, or any fever >39 °C.
- **Facial/Head Pain or Tenderness**: Intense sinus pain, forehead/cheek pressure or swelling (possible sinusitis/abscess).
- **Purulent Nasal Discharge**: Thick, colored mucus >7–10 days (could signal bacterial sinusitis).
- **Severe Cough or Difficulty Breathing**: Wheezing, shortness of breath, chest pain (rule out bronchitis/pneumonia/asthma/COVID).
- **Ear Pain or Hearing Loss**: (Possible otitis media from cold).
- **Neurologic or Vision Changes**: (Meningitis or other rare complications).
- **Immunocompromise or Pregnancy**: Lower threshold for medical evaluation (some “natural” remedies unsafe; consider antivirals if influenza/COVID risk).
- **Dehydration Risk**: Inability to tolerate fluids, faintness, or confusion.

Always use sterile (boiled/distilled) water for nasal rinsing.  Avoid nasal corticosteroids/antihistamines for immediate relief (they take hours to days to work) – these are standard treatments if symptoms persist beyond 48 h.

**Recommendation:** For rapid relief in acute rhinitis, we recommend (with moderate confidence) **nasal saline irrigation and adequate hydration** as first-line safe measures.  *Supplement with zinc lozenges* (started within 24 h) as there is low-certainty evidence of ~2-day duration shortening, acknowledging GI side effects.  Honey can be used for cough.  We caution that most “natural” remedies lack strong evidence; thus, rely primarily on symptomatic relief and watch for signs to consult a doctor if needed.  This plan assumes the case is an ordinary adult (no pregnancy, no immunosuppression).

**Sources:** Cochrane/Systematic reviews and guidelines as cited above.

---

**Claude:**

{"lang":"en","topic":"Acute rhinitis (runny nose, sneezing): evidence for self-care and natural remedies","one_line":"What evidence supports natural and self-care measures for rapid (0–48 h) relief of acute rhinitis (allergic, viral or irritant) in an ordinary adult, and which popular remedies lack support?","key_findings":["Symptoms of sudden sneezing, watery rhinorrhea and congestion without sore throat point to allergic, viral (common cold) or irritant/nonallergic rhinitis. Allergic rhinitis features itch and no fever; a cold is self-limited at about 5–10 days, peaking around day 2–3; irritant rhinitis tracks exposure and lacks itch and IgE markers.","No natural remedy has solid evidence of rapid (24–48 h) relief, and claims of a '1–2 day cure' are unsupported. Studies measure duration in days or symptom scores, not immediate cure.","Nasal saline irrigation or spray and adequate hydration are the safest first-line measures. RCTs suggest saline gives symptom relief in colds and sinusitis, and the report rates them 'established' and recommends them with moderate confidence. Use distilled or boiled (cooled) water.","Zinc lozenges (about 75 mg/day or more) started within 24 h of onset may shorten a cold by about 2 days (MD -2.37 d; CI -4.21 to -0.53). Evidence is low-certainty and side effects include nausea and taste disturbance. Zinc does not prevent colds. Intranasal zinc is unsafe (FDA warning, permanent anosmia), and long-term doses should stay under 40 mg/day to avoid copper deficiency.","Honey (1–2 teaspoons, alone or in warm tea) soothes cough and sore throat, mostly shown in pediatric studies. It is not proven for congestion and must never be given to infants under 1 year (botulism risk).","Some herbal products show modest, low-quality benefit. Andrographis shortens colds by about 1 day, Pelargonium sidoides (EPs 7630) has very-low-quality evidence with improvement by day 10 but not day 5, and elderberry syrup is preliminary. Butterbur (PA-free only, hepatotoxicity risk) and curcumin help allergic rhinitis over weeks, not acute colds.","Echinacea shows no consistent benefit and homeopathy performs no better than placebo. Garlic has one small prophylaxis trial (n=146) and no acute evidence. Vitamin C helps only as daily prophylaxis, shortening colds by about 8% (about 0.5 day), with minimal effect when started after onset. Steam and essential oils give comfort only, and hot steam can burn. The 'milk causes mucus' belief has no clinical support.","Antihistamines and nasal steroids are effective for allergic rhinitis but need hours to days, so they are not instant cures. They are the standard option if symptoms persist beyond 48 h.","Red flags for medical care: fever above 38.5 °C for more than 3 days or above 39 °C, severe facial pain, purulent discharge for more than 7–10 days, wheezing or dyspnea, ear pain, neurologic or vision changes, dehydration, and pregnancy or immunocompromise."],"recommendations":["Start with hydration and rest, plus isotonic saline spray or irrigation 1–2 times a day using sterile, distilled or boiled-cooled water.","Optionally add zinc gluconate lozenges (about 13–23 mg each, about 75 mg/day total) only if started within 24 h of onset. Stop if there is nausea or a bad taste, and never use intranasal zinc.","Use honey (1–2 teaspoons) for cough or throat irritation in anyone over [ВОЗРАСТ].","Use warm fluids, warm (not scalding) steam, menthol rub or chamomile or ginger tea for comfort only, and avoid garlic, onion or essential oils in the nose.","Do not rely on echinacea, homeopathy, high-dose vitamin C after onset or other unproven remedies, and do not overconsume supplements.","Most colds improve in 5–7 days. See a clinician if there is no improvement in 7–10 days or if any red-flag sign appears.","Move to antihistamines or nasal steroids if symptoms persist beyond 48 h, since they are the standard allergic rhinitis treatment."],"entities":{"people":["Hemilä"],"companies":["Cochrane","NCCIH","FDA"],"products_tools":["Nasal saline spray/irrigation (neti pot)","Zinc gluconate lozenges","Honey","Vitamin C","Echinacea","Elderberry (Sambucus) syrup","Andrographis (Kan Jang)","Pelargonium sidoides (EPs 7630)","Butterbur (PA-free)","Curcumin/turmeric","Nigella sativa (black seed)","Probiotics","Antihistamines","Nasal corticosteroids","Humidifier/steam inhalation","Menthol/eucalyptus rubs"]},"open_questions":["Do any herbal remedies give true rapid (24–48 h) relief? Placebo-controlled trials measuring 24–48 h symptom scores are lacking.","What are the standardized doses and preparations for herbal extracts, given their high variability?","Does zinc truly shorten colds? The evidence is low-certainty and dose and formulation dependent.","Are probiotics useful for acute URTI duration or incidence? Heterogeneity is high and preparations vary.","Do the findings apply beyond the assumed ordinary adult (no pregnancy, no immunosuppression)? The report's sources are cited only generally as 'Cochrane/Systematic reviews and guidelines', not itemized.","How should one tell allergic from viral or irritant cause in an individual case without testing (IgE, nasal smear)?"],"related_concepts":["Allergic rhinitis","Common cold / viral URTI","Nonallergic (irritant) rhinitis","Nasal saline irrigation","Zinc lozenges and cold duration","Evidence-based natural remedies","Placebo effect and homeopathy","Red flags / when to seek care","Antihistamines and intranasal steroids","Herbal supplement safety"]}
