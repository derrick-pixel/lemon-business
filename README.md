# Lemon Business — Counterparty Lemon Platform

Marketing site for **Lemon Business**, a concept-stage B2B counterparty-reputation
venture in Singapore. A peer-sourced check on the SME owners and businesses you
trade with, built around the **Lemon Score** — a demerit engine where high = sour
(a risky counterparty), low = peach (safe to deal with).

Sibling of **Lemon Man** (the worker-screening original). Same design system and
scoring engine, recalibrated from workforce reliability to **B2B trade behaviour**:
late payment, bad-faith invoice disputes, legal-threat bullying, undelivery,
NDA/IP breaches, phoenixing, and the rest. This is peer review *of business owners
by the businesses who dealt with them* — not ex-staff reviewing employers (that's
what Glassdoor and Google Maps already do).

> **Status: concept-stage, not launched.** Public-facing marketing site, built as a
> design artefact. Every page carries `noindex, nofollow`. See *Going live* before
> changing that.
>
> **⚠️ Legal note.** A peer-review reputation product carries real defamation /
> POHA exposure in Singapore (there is no anti-SLAPP shield). The design hinge that
> keeps it defensible: every entry is a **dated, evidenced incident keyed to a UEN**
> — a fact, not an opinion — plus a paid-upload filter, a contest window, and
> corroboration weighting. Do not publish without the venture's lawyers clearing
> this build.

## Stack

Static HTML/CSS/JS — no build step, no dependencies. dt-site-creator methodology:
multi-page scaffold, shared design system, OG/social meta, adaptive SVG favicon,
cache-busted includes (`?v=1`).

## Pages

| File | Purpose |
|---|---|
| `index.html` | Hero, the lemon economics (Akerlof), two problems, the Lemon Score, hard/soft power, lemon-detector scoreboard |
| `how-it-works.html` | The Lemon Score engine — incident points, the quadratic corroboration multiplier, decay, the 24–72h contest window |
| `for-businesses.html` | "Un-lemon yourself" — the alert, contesting, ripening back to peach, the free independent appeal |
| `pricing.html` | Lemon tokens, monthly plans, free appeals, the >10-lemons-a-quarter self-check rule |
| `trust.html` | "The Squeeze" — paid uploads, contest window, Mutually Assured Sourness, corroboration, UEN-keyed evidence |
| `simulator.html` | The full ~48-incident catalogue across six categories, same engine as the calculator |

```
assets/
  css/lemon.css      design system (citrus B2B, Lemon Score = sour-high)
  js/lemon.js        nav, scroll-reveal, Lemon Score gauge + meter, calculator + simulator engine, form stub
  data/confessions.json  rotating counterparty "confessions"
  img/favicon.svg    filled-lemon monogram
  img/og-image.png   1200×630 social card  (regenerate: scripts/generate-og.py)
scripts/
  generate-og.py     PIL-based OG card generator (rerunnable)
```

## Run locally

```
python3 -m http.server 8000   →   http://localhost:8000
```

## The Lemon Score (B2B calibration)

0–1000 demerit scale. High = lemon (risky), low = peach (safe to deal with).
~48 incident types across six categories:

1. **Payment & financial reliability** — chronic late payment, term-stretching, bad-debt default, deposit-and-disappear
2. **Litigiousness & intimidation** — vexatious letters of demand, defamation/POHA threats to silence feedback
3. **Service, quality & delivery** — undelivery, substandard work, abandonment, counterfeit goods
4. **Integrity & good faith** — reneging on agreed deals, NDA/IP breach, poaching, kickbacks
5. **Operational & structural red flags** — phoenix companies, serial struck-off directors, GST/tax non-compliance, unlicensed operation
6. **Communication & conduct** — ghosting, moving the goalposts, misrepresentation, fabricated references

Each incident scores `base × m(n)`, where `n` is the number of independent
businesses that logged it and `m(n) = 0.25n² + 0.75n` (×1, ×2.5, ×4.5). Ripening
offsets — verified trade references, industry accreditation, settling overdue
invoices, clean time — decay it back down. Engine lives in `assets/js/lemon.js`.

**Identifier:** business name + **UEN** + named directors (ACRA BizFile / data.gov.sg),
not NRIC. The UEN is the public join key that binds a record to a court-defensible
identity.

## Calibration sources

Base severities and the incident taxonomy are grounded in Singapore B2B payment
and counterparty-risk data (Atradius *Payment Practices Barometer* SG 2024/2025 —
~35% of B2B sales paid late, bad-debt write-offs rising 4%→6%; InvoiceInterchange
SG SME cashflow; ACRA director-disqualification rules; POHA / defamation context).
Headline stats are industry-reported survey panels, framed as such on the site.

## Design

Inherited from Lemon Man: playful citrus B2B — warm cream paper, deep ink, hard
borders with offset shadows. Lemon amber = the "sour / bad" signal; peach-coral =
clean / good. Fraunces (display) + Hanken Grotesk (body) + Spline Sans Mono (data).
Deliberately not Elitez navy — positioned as an independent venture.

## Going live

Currently `noindex` and held pending **legal sign-off on this build**. To publish:
get the lawyers' clearance, remove `noindex, nofollow` from every page `<head>`,
bump the `?v=` cache-bust, confirm GitHub Pages.

---
Concept-stage venture. Confidential.
