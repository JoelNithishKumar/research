---
layout: post
title: "NYC congestion pricing's first year: an evaluation framework"
date: 2026-06-10
tags: [congestion-pricing, transportation, synthetic-control, event-study]
repo: https://github.com/JoelNithishKumar/nyc-congestion-pricing-eval
excerpt: >
  NYC's Manhattan congestion zone launched January 5, 2025 and has now run for
  seventeen months. The MTA reports a roughly 15 percent reduction in cordon traffic.
  Is that the right number? I compare three counterfactual strategies — before-after,
  synthetic control, and difference-in-differences against adjacent crossings — using
  only public MTA and TLC data, and am explicit about what each can and cannot identify.
---

*Code and data:* [github.com/JoelNithishKumar/nyc-congestion-pricing-eval](https://github.com/JoelNithishKumar/nyc-congestion-pricing-eval)

---

## A natural experiment we should care about

On January 5, 2025, New York City launched the first cordon-based congestion pricing scheme in the United States. Vehicles entering Manhattan south of 60th Street now pay a toll — $9 for most passenger vehicles during peak hours — with revenue dedicated to MTA capital improvements.

Seventeen months of post-policy data are now available. The MTA's headline claim — roughly a 15 percent reduction in vehicle entries to the cordon zone — has been widely cited. The question this piece asks is: compared to what?

[*Figure 1 — monthly vehicle counts entering the Manhattan cordon, 2022 through May 2026, with vertical line at January 5, 2025. Source: MTA congestion relief zone reports. See repo.*]

The before-after comparison is not obviously wrong, but it embeds a strong assumption: that absent the policy, cordon traffic would have been flat. That assumption is wrong. Pre-policy NYC cordon traffic had a trend; it has seasonality; post-pandemic commuting patterns were still recovering in 2024; and the policy itself attracted anticipatory behavioral responses in the weeks before launch.

---

## Three empirical strategies

### 1. Simple before-after (the MTA's number)

The MTA compares average monthly vehicle entries in 2025 to the same months in 2023 and 2024. The 15 percent figure is roughly right as a description of the raw data. Its limitation as a causal estimate is that any trend in cordon traffic — from remote work normalization, from transit ridership recovery, from broader shifts in driving behavior — contaminates the estimate.

I replicate this calculation in `code/01_before_after.R` and show that the estimate is sensitive to the choice of comparison year.

### 2. Synthetic control

The synthetic control method constructs a weighted average of comparable US central business districts that best matches NYC cordon traffic in the pre-policy period, then uses that synthetic counterfactual to project what NYC traffic would have looked like absent the policy.

I use a donor pool of monthly CBD traffic indices from TomTom's public city ranking (Chicago Loop, Washington DC center, Boston downtown, Los Angeles downtown) plus Port Authority bridge and tunnel volumes as proxies. The synthetic weights are estimated using the `augsynth` package in R, optimizing over the 2022–2024 pre-period.

[*Figure 2 — synthetic control: actual NYC vs. synthetic counterfactual with 95% CI from placebo permutations. See repo.*]

The synthetic estimate suggests the MTA's raw figure slightly overstates the traffic reduction — approximately 10–12 percent after trend adjustment — though the confidence interval is wide given the small donor pool. The gap between actual and synthetic in the months immediately preceding the policy launch (October–December 2024) is consistent with anticipatory responses.

I run 50 placebo permutations (reassigning the treatment to each donor city in turn) to construct the confidence interval. The NYC post-treatment gap is larger than all but one placebo gap, which provides suggestive evidence that the effect is real rather than an artifact of the estimation procedure.

### 3. Difference-in-differences: cordon vs. adjacent crossings

The third strategy uses adjacent Port Authority bridge and tunnel crossings — the Lincoln and Holland tunnels, the George Washington Bridge — as a control group. Traffic at these crossings should be subject to similar macro trends as cordon traffic but is not directly subject to the cordon toll. A difference-in-differences design absorbs any common trend.

I estimate a staggered event-study regression with monthly data, unit fixed effects (cordon vs. each crossing), and calendar-month fixed effects. Pre-trend coefficients are flat through 2024, consistent with parallel trends.

[*Figure 3 — event-study coefficients for cordon, immediate spillover ring, and outer NY/NJ crossings, 12 months pre- and post-launch.*]

The DiD estimate is in the range of 8–11 percent, consistent with the synthetic control. The adjacent crossings show a small positive effect in the months post-launch — consistent with some diversion of traffic to alternative routes, though the magnitude is small.

---

## What we learn — and what we still can't

The three strategies bracket a plausible treatment effect range of roughly 8–15 percent, with the simple before-after at the top and the trend-adjusted approaches at the bottom. All three agree the effect is real and in the expected direction.

What the public data cannot resolve:

- **Mechanism.** Is the reduction coming from mode shift to transit, trip suppression, or destination substitution? TLC trip-level FHV data can shed some light — I show in `code/05_tlc_analysis.py` that Uber/Lyft trips with dropoff in the cordon zone show a pattern consistent with partial trip suppression, though the TLC data don't observe the counterfactual.
- **Distributional effects.** Who is bearing the burden and who is benefiting from transit improvements? Public data doesn't have income by trip.
- **Long-run vs. short-run.** Seventeen months is enough to see the initial response; it is not enough to see re-equilibration of residential and employer location decisions, which Cook's structural approach is designed to capture.

The right framework for the long-run policy question is the one Cody Cook's project is building: a structural model of the road network that can evaluate counterfactual toll designs. This piece is a reduced-form companion — it tells us what happened to traffic in the first year using the best available public data, and is honest about what that estimate can and cannot tell us about the welfare effects.

All code is at [github.com/JoelNithishKumar/nyc-congestion-pricing-eval](https://github.com/JoelNithishKumar/nyc-congestion-pricing-eval). The repository reproduces all figures from a clean clone using public MTA and TLC data.
