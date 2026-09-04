# PhonePe — Trust in the Money Gap

**A product case study on the moment between "debited" and "credited."**

When a UPI payment fails on PhonePe, the money is usually already on its way back — automatically, inside a regulated deadline, with no action needed from the user. The app tells them none of that. It shows "Failed" and a spinner.

This study argues that the gap is not refund speed. It's silence.

---

## The finding

I went in expecting to find slow refunds. I found the opposite.

- **RBI mandates auto-reversal** within T+1 day for person-to-person UPI transfers and T+5 for merchant payments, with ₹100 per day of compensation for delay — payable without the user filing a claim.
- **In my survey, every reported incident resolved fast**: of 9 affected users, 4 were same-day, 4 within 1–3 days, 1 within 4–7. Nobody came close to the 3–10 day window PhonePe discloses.
- **Yet anxiety ran nearly double** that of unaffected users (3.1 vs 1.75 on a 1–5 scale), and **only 1 of the 9 could find out what was happening without contacting support**.
- **4 of the 9 contacted support anyway** — for a process that was already running without them.

The system works. The user has no way to know. That reframes the problem from an SLA question into a communication question, which is a dramatically cheaper category of fix.

## The second finding

The payment rails already carry everything needed to fix it.

NPCI's **UDIR** framework (Unified Dispute and Issue Resolution, 2020) polls transaction status continuously, auto-routes disputes to the responsible party, and pushes status updates and refund confirmation back to the payer's app. NPCI's own circular already **requires** payer apps to support in-app dispute raising.

An independent Dvara Research study of six UPI apps found only four allowed in-app complaints at all. Grievance options sat a level deeper in transaction history, often in a screen corner. One issued no ticket number. None displayed complaint status or expected turnaround time prominently.

So this isn't a bank-integration project. It's a presentation-layer gap that any app could close, and none has.

---

## What I proposed

| Solution | Priority | Why |
|---|---|---|
| **Refund Guarantee Timer** | P0 | Surfaces a policy and a statutory entitlement that already exist. No new data dependency. |
| **Live Money Trail** | P0 | Renders the stage status UDIR already delivers: Debited → In transit → At recipient's bank → Credited or Reversed. |
| **One-Tap Dispute** | P1 | NPCI already mandates in-app disputes. Pre-fills data PhonePe already holds; returns a trackable ticket ID. |

**North Star:** Post-Failure Trust Recovery Rate — the share of users who return to their pre-incident transaction frequency within 30 days of a failed payment.

Each solution slide names its own constraint, because they matter:
- In merchant flows NPCI returns only success or failed, with no intermediate state — so the trail must degrade honestly rather than invent a stage it cannot verify.
- The ₹100/day compensation is owed by the **bank**, not PhonePe, which is a TPAP rather than the account holder's bank. The feature discloses and tracks the entitlement; it cannot promise to pay it.
- Goods and merchant disputes route through the user's bank or NPCI as a chargeback under PhonePe's own Grievance Policy §7. One-Tap Dispute is scoped to payment failures only.

---

## How I researched it

**1. Primary pulse survey.** Google Form distributed through WhatsApp groups, classmates and family contacts, 4–9 August 2026. 20 responses, 13 confirmed current PhonePe users. Raw responses included in this repo.

**2. Official documentation.** PhonePe's published Grievance Policy (16 July 2026) and merchant documentation on failed UPI transactions — used to establish refund windows, liability limits and escalation paths from primary sources rather than assumption.

**3. Regulatory and network review.** RBI's Turn Around Time circular (DPSS.CO.PD No.629/02.01.014/2019-20), RBI's Online Dispute Resolution circular, and NPCI's UDIR circular.

**4. Complaint and benchmark review.** Publicly available complaints scanned qualitatively for recurring failure patterns. App-level comparison cited from Dvara Research's published six-app study rather than a self-run teardown.

**5. Prototype.** An interactive clickable prototype of all three solutions, built in vanilla HTML, CSS and JavaScript.

---

## Limitations

Stated plainly, because they shape what the study can and cannot claim:

- **n=20 is directional, not statistically powered.** Respondents came from my own network — urban, salaried, and with **no merchant respondents at all**. An earlier draft included a small-merchant persona; it was cut, because I had no merchant evidence to support it.
- **The anxiety question was conditional but answered by every respondent**, so the 1.75 baseline reflects anticipated rather than experienced anxiety.
- **Recommendation intent was measured 1–5 and is not NPS.** And it came back essentially flat: 3.4 among affected users versus 3.5 among unaffected. Users reported real anxiety but did not report being less willing to recommend PhonePe. That finding cuts against my own thesis, and it's the reason the North Star is defined behaviourally rather than as a sentiment score.
- **Complaint review was qualitative scanning**, not a quantified sample. No frequency distribution is claimed.
- **App-level benchmarking is cited from a 2023 third-party study** and was not independently re-verified. That study anonymises the apps, so no claim is made about which one is PhonePe.
- **The prototype has not been user-tested.**

---

## What I'd do next

1. **Scale the survey to 100+ screened respondents outside my own network**, and recruit small merchants specifically — the largest untested claim adjacent to this study.
2. **Validate the UDIR assumption with a TPAP engineer.** The effort estimate for the Live Money Trail rests on what status data actually reaches a payer app in practice, not on what the circulars permit. Confirming it would either strengthen or collapse the P0 call.
3. **User-test the prototype** with 5 people who have experienced a failure, and measure whether self-reported anxiety falls from the 3.1 baseline.
4. **Instrument the thesis behaviourally** — transaction-frequency data on affected users against a matched control. Until that exists, the North Star is a proposal rather than a validated metric.

---

## Files

| File | What it is |
|---|---|
| The full 17-slide deck |
| `https://docs.google.com/spreadsheets/d/1It35vZ_uJu69zzFFPzuZmDSu6Obug80P8GQd2sxMBmE/edit?usp=sharing` | Raw survey responses (20 rows) |


---

## Sources

All figures in the deck trace to one of the following:

- PhonePe Updated Draft Red Herring Prospectus, filed with SEBI 21 January 2026
- PhonePe Grievance Policy, dated 16 July 2026 — `phonepe.com/grievance-policy`
- PhonePe merchant documentation on failed UPI transactions — `business.phonepe.com`
- RBI, *Harmonisation of Turn Around Time and Customer Compensation for Failed Transactions*, September 2019
- RBI, *Online Dispute Resolution System for Digital Payments*, August 2020
- NPCI, *UDIR — Enhancing Complaint Handling & Resolution Process for UPI Transactions*, November 2020
- NPCI app-level UPI ecosystem statistics
- Dvara Research, *Do UPI In-App Grievance Redress Mechanisms work for constrained users?*, March 2023

> **Note on currency:** market-share percentages move month to month, and PhonePe's IPO was postponed in March 2026 with no confirmed date at the time of writing. Verify both before citing.

---

## About

Independent product case study by **Nehal Chaudhary** — a solo exercise covering research, persona work, prioritisation and prototyping. Not affiliated with or endorsed by PhonePe.

Netaji Subhas University of Technology · [nehal.chaudhary.ug23@nsut.ac.in](mailto:nehal.chaudhary.ug23@nsut.ac.in)
