---
layout: post
title: "The geography of the delivery markup: a research design note"
date: 2026-06-17
tags: [platform-pricing, price-discrimination, cost-of-living, design-note]
repo: https://github.com/JoelNithishKumar/delivery-markup-project/tree/main
excerpt: >
  Does the markup that food-delivery platforms charge over in-store menu
  price vary systematically with neighborhood income — and if so, does that
  pattern look more like willingness-to-pay price discrimination, or like
  platforms extracting more where consumers have fewer alternatives? This is
  a design note: the data infrastructure is built, price collection is in
  progress, and results will follow.
---

*Status: design and data infrastructure complete; price collection in progress. Full results to follow.* &nbsp;·&nbsp; [Repository](https://github.com/JoelNithishKumar/delivery-markup-project/tree/main) &nbsp;·&nbsp; [Full design note](https://github.com/JoelNithishKumar/delivery-markup-project/blob/main/writing/design_note.md)

---

## The question

Within a single U.S. metro area, does the markup that food-delivery platforms like DoorDash and Uber Eats charge over in-store menu price vary systematically with neighborhood income — and does the direction of that relationship look more consistent with **willingness-to-pay price discrimination**, or with **platforms exploiting limited consumer alternatives** in underserved areas?

A useful research design needs to do more than detect a correlation between markup and income. It needs to discriminate between two theories that make opposite, falsifiable predictions:

- **Willingness-to-pay discrimination.** If higher-income neighborhoods have more inelastic demand for delivery — time is more valuable, there are fewer easy substitutes for ordering in — a profit-maximizing platform should set *higher* markups where income is higher. This is third-degree price discrimination, applied to a digital intermediary.
- **Access exploitation.** If lower-income neighborhoods have fewer competing delivery options, less car access, or fewer easy substitutes for picking food up themselves, the platform can extract *more* markup precisely where consumers have the fewest alternatives — predicting markup *falls* with income.

The sign of the income gradient, once local competition is controlled for, is what lets the data adjudicate between these two stories rather than just describing a correlation.

## Why this matters

This sits at the intersection of two active areas in applied microeconomics. Work on spatial retail access has shown that *which retailers people can actually reach* drives real cost-of-living differences across neighborhoods that standard price indices miss. If delivery platforms layer a geographically uneven markup on top of that existing gap — and the share of consumption flowing through delivery platforms keeps growing — official cost-of-living measures may be missing a real and widening wedge.

It's also a clean test case for platform market power: a setting where the same product, from the same chain, is sold at two prices in the same week, and the only thing that varies is the customer's neighborhood.

## Design

**Geography.** Chicago, IL. Twenty ZIP codes (ZCTAs), stratified into income terciles (7 low, 7 mid, 6 high) using 2018–2022 ACS 5-year estimates, after excluding low-population downtown/commercial ZCTAs that aren't representative residential neighborhoods.

**Neighborhood covariates.** Median household income and population pulled from ACS via `tidycensus`; population density computed by joining to the Census Gazetteer ZCTA file. This panel is already built.

**Price data.** Five national quick-service chains chosen for menu standardization across locations — McDonald's, Chipotle, Domino's, Panda Express, Subway. One anchor item per chain, collected by hand across all 20 ZIPs: in-store menu price versus app price (DoorDash, Uber Eats), recorded *before* delivery and service fees, to isolate the markup on the item itself rather than the all-in cost of delivery.

**Market structure control.** Number of quick-service delivery options visible on a single platform's feed per ZIP, used as a proxy for local competitive intensity.

**Planned specification:**

```r
m2 <- feols(markup_pct ~ log(median_income) + density + n_competitors_visible | chain,
            data = prices, cluster = "zip")
```

Chain fixed effects absorb baseline markup differences across chains; standard errors are clustered at the ZIP level. The coefficient on `log(median_income)` — after controlling for competition — is the key object. Positive and robust favors discrimination; negative and robust, especially if it *strengthens* once competition is added, favors access exploitation.

## What's built, what's left

The ACS/Gazetteer panel, the 20-ZIP stratified sample, and the full price-collection instrument are done. What remains is manual price collection across the 100 ZIP × chain anchor-item observations. Regression results, figures, and the completed write-up will follow as collection finishes.

## Limitations, stated up front

This is a single-metro design — it describes Chicago, not a national pattern. Manual price collection introduces some measurement noise relative to a scraped dataset, though the collection protocol (item-only, pre-fee price) is fixed in advance to minimize inconsistency. And the cross-sectional design is descriptive, not causal: it's built to characterize the pattern cleanly, not to establish platform intent on its own — that would need something like a platform fee-policy change as a natural experiment.

The full design note, data, and collection instrument are at [github.com/JoelNithishKumar/delivery-markup-project](https://github.com/JoelNithishKumar/delivery-markup-project/tree/main).
