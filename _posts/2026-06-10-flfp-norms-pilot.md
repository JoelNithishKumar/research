---
layout: post
title: "Misperception and norms in female labor force participation: a pilot information experiment"
date: 2026-06-10
tags: [gender, labor-economics, survey-experiment, india]
repo: https://github.com/JoelNithishKumar/FLFP-Norms-Pilot/tree/main
excerpt: >
  India's female labor force participation rate has grown faster than almost
  any country on earth over the past decade  yet still sits near the bottom
  of the global distribution in absolute terms. A pilot survey experiment
  asks whether showing people this number changes their beliefs, and finds
  that "misperception" depends entirely on which official statistic you treat
  as ground truth.
---

*Code, data, full article, and slides:* [github.com/JoelNithishKumar/FLFP-Norms-Pilot](https://github.com/JoelNithishKumar/FLFP-Norms-Pilot/tree/main)

---

## Two true statements that sound contradictory

Between 2015 and 2025, India's female labor force participation rate (FLFPR) grew faster than the FLFPR of all but a handful of the 181 countries with usable World Bank/ILO data  landing at the **97th percentile** of global growth.

Over the same period, India's FLFPR *level* sits at only the **11.5th percentile** globally  among the lowest in the world, growth notwithstanding.

<img src="/research/assets/img/flfp-norms-pilot/fig1_global_growth_distribution.png" alt="Distribution of female LFPR growth across 181 countries, 2015 to 2025, with India marked at the 97th percentile" style="max-width:100%; margin: 1rem 0;">

Both facts are correct. This is the classic low-base pattern: a large percentage change from a small starting point is still consistent with a small absolute level. The question this project asks is what happens when you put a number  any number  in front of people who are trying to assess how India is doing on this measure, and how much that assessment depends on which official statistic you hand them.

---

## Where India sits among comparable countries

Placed alongside other countries with broadly similar income and demographic profiles, India's recent FLFPR growth looks more like Saudi Arabia's or Bolivia's than like its South Asian neighbors. But the comparison that matters more for everyday perception is probably the regional one  and there, the picture is less flattering.

<img src="/research/assets/img/flfp-norms-pilot/fig4_south_asia_comparator.png" alt="Female labor force participation rate across South Asia in 2024, with India below the world average" style="max-width:100%; margin: 1rem 0;">

Among five South Asian countries with comparable World Bank/ILO estimates for 2024, India sits in the middle  well below the global average of roughly 51 percent, and below Bangladesh specifically, despite India's much faster recent growth rate.

---

## The pilot: does showing people the number change anything?

The second half of the project is a small pilot survey experiment (N = 9, three arms) testing whether exposure to India's actual FLFPR shifts respondents' beliefs and attitudes about female labor force participation. The pilot is intentionally underpowered  nine respondents is not a sample size you draw policy conclusions from  but it surfaces a measurement issue that matters regardless of sample size.

Respondents in the arm asked to guess India's FLFPR before any information was shown produced estimates that were, on average, close to the World Bank/ILO modelled estimate for India.

<img src="/research/assets/img/flfp-norms-pilot/fig5_pilot_vs_global_relationship.png" alt="Density plot comparing where pilot respondents guessed India's female labor force participation rate stood against the true World Bank ILO value and against the global distribution" style="max-width:100%; margin: 1rem 0;">

That calibration looks very different depending on which "true" value you compare it to. Against the World Bank/ILO series, respondents were nearly spot on. Against India's own national Periodic Labour Force Survey (PLFS) statistic  which uses a different survey design and tends to report a higher FLFPR  the same guesses would read as a sizeable underestimate.

In other words: whether ordinary people "misperceive" India's FLFPR is not just a fact about their beliefs. It is also a fact about which of two legitimate, differently-constructed official statistics gets treated as the benchmark. Cross-national series like the World Bank/ILO panel and within-country administrative series like the PLFS are not measuring exactly the same thing, and conflating them produces a misperception finding that may be more about measurement than about belief.

---

## What this leaves open

The pilot's job was to surface this measurement issue before scaling up, not to settle it. A well-powered follow-up would need a larger sample, a cleaner pre-registered design, and an explicit choice  stated up front  about which statistic counts as ground truth and why. The state-level data on rural FLFPR (Periodic Labour Force Survey via Ravi and Kapoor, 2024) suggests there is also enormous within-India variation hiding underneath the national number, which is a separate question worth its own design.

All code, the full written article with citations, the complete set of figures, and a slide deck walking through the analysis are at [github.com/JoelNithishKumar/FLFP-Norms-Pilot](https://github.com/JoelNithishKumar/FLFP-Norms-Pilot/tree/main). The repository reproduces every figure and table from raw data using base R only.
