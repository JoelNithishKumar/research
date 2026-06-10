---
layout: post
title: "Administrative burden and SNAP take-up: a state-panel revisit"
date: 2026-06-10
tags: [snap, safety-net, public-economics, event-study]
repo: https://github.com/JoelNithishKumar/snap-takeup-revisit
excerpt: >
  How much of the across-state variation in SNAP take-up in 2018–2023 can be
  attributed to differences in administrative burden? I build a state-year panel
  from USDA and ACS data, estimate cross-sectional OLS and an event study around
  the 2022–2023 unwinding of pandemic interview waivers, and am explicit about
  what each specification can and cannot identify.
---

*Code and data:* [github.com/JoelNithishKumar/snap-takeup-revisit](https://github.com/JoelNithishKumar/snap-takeup-revisit)

---

## The puzzle

SNAP take-up rates vary dramatically across states — USDA data puts the range at roughly 60 to 100 percent of eligible households in recent years. Some of that variation is demographic. A substantial share, the recent literature argues, is administrative: how hard a state makes it to apply and stay enrolled.

[*Figure 1 here — SNAP take-up by state, most recent year. See repo for code.*]

A 30-point gap in take-up is not a marginal policy parameter. It means that in low-take-up states, a large fraction of eligible households — disproportionately low-income, food-insecure — are not receiving the benefits the program was designed to deliver. Understanding why matters for both program design and for evaluating the redistributive impact of the safety net.

---

## What we know from the literature

The modern administrative burden literature dates the sharpest results to the mid-2010s. Homonoff and Somerville (2021) use a quasi-experimental design around SNAP recertification policy changes and find meaningful effects on participation rates. Finkelstein and Notowidigdo (2019) estimate that improving take-up of SNAP through information and application assistance has welfare effects comparable to benefit increases. Deshpande and Li (2019) show, in the SSI context, that closing Social Security field offices — a supply-side shock to administrative access — reduces program participation significantly and persistently among elderly applicants.

The Wallace and Ndumele research program extends this logic to Medicaid, where the administrative machinery is richer and state-level variation more granular. The SNAP setting is complementary: the federal structure creates clean policy variation across states, and the pandemic produced a natural shock to that variation.

---

## Data construction

I construct a state-year panel for 2018–2023 from four sources:

1. **USDA SNAP State Activity Reports** — annual program participation counts by state.
2. **USDA SNAP Policy Database** — state-level policy options including recertification periods, interview requirements, and online application availability.
3. **USDA Program Access Reports** — state-level participation rates as a share of estimated eligible households.
4. **American Community Survey (IPUMS USA)** — eligibility denominators based on income and household composition.

The administrative burden index combines three binary components: whether in-person interview is required for initial application, whether telephone interview is required for recertification, and whether a fully online application pathway exists. The index runs 0–3, with higher values indicating greater burden.

Construction details and all merge decisions are documented in `code/01_build_panel.R` in the repository.

---

## Cross-state regressions

Table 2 (see repo) reports OLS estimates of the burden index on state-level SNAP take-up, with and without state and year fixed effects. The within-state coefficient — the association between changes in a state's burden index and changes in its take-up rate — is negative and economically meaningful, in the range of 3–5 percentage points per unit increase in the burden index.

I am explicit that this is *not* a causal estimate. State policy is endogenous to state preferences for redistribution: the same political economy that produces high burden may independently depress take-up through other channels. The OLS panel tells us the correlation is stable and robust to controlling for state and year effects; it cannot rule out unobserved confounders that move with policy.

---

## Event study: the 2022–2023 unwinding of pandemic waivers

The stronger identification comes from an event study around the rollback of pandemic SNAP waivers. During COVID-19, most states received USDA waivers suspending in-person and telephone interview requirements. Those waivers were lifted at staggered times across states beginning in mid-2022 and continuing through 2023 — a near-textbook staggered policy reversal.

I estimate the event study by regressing state-month take-up on event-time indicators (six months before through twelve months after the waiver lift), with state and calendar-month fixed effects. Standard errors are clustered at the state level. Because 50 clusters is on the small side for cluster inference, I also report wild cluster bootstrap p-values as a robustness check.

[*Figure 3 here — event-study coefficients with 95% CIs. Horizontal axis: event time in months. Vertical: change in take-up. See repo.*]

The pre-trend coefficients are flat (parallel trends passes visual inspection in the pre-period). Post-lift, take-up falls measurably in the first six months, consistent with the administrative friction hypothesis. The estimates are noisier than I would like — 50 clusters is a genuine limitation — but the direction is consistent with the OLS panel and with the experimental literature.

---

## What this means

The honest summary is that public, state-level data can establish a robust negative correlation between administrative burden and take-up, and that the pandemic waiver variation provides suggestive quasi-experimental evidence in the same direction. What it cannot do is pin down the mechanism (is it the application cost, the recertification cost, or the information about eligibility?) or produce estimates precise enough for welfare analysis.

The natural next step would be state-level administrative microdata — individual spell records that let you observe transitions into and out of the program, not just stock take-up rates. That is exactly the kind of data that Wallace and Ndumele's SCALE-Connecticut work accesses. A careful reduced-form piece using spell-level records, with the staggered waiver rollback as the identifying variation, would be far more informative than what I can do with public data alone.

All code is at [github.com/JoelNithishKumar/snap-takeup-revisit](https://github.com/JoelNithishKumar/snap-takeup-revisit). The repository reproduces all tables and figures from a clean clone.
