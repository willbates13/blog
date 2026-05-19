---
title: "Strokes Gained: Why It's the Best Stat in Sports"
date: 2026-05-15
tags: ["PGA Tour", "strokes gained", "statistics"]
summary: "Strokes Gained is the cleanest sport-wide measurement framework in professional sports. Here's the math behind it and how I'm using it to build a course-fit model."
sport: "golf"
---

## The Core Idea

Every shot in professional golf can be assigned an expected score from that position. SG measures how much better (or worse) than expected a player performs.

A 10-foot putt has an average make rate of ~40% on the PGA Tour, so it's worth -1.4 strokes from the hole. If you make it, you gained +0.4 strokes vs the field. If you miss and two-putt, you lost -0.6 strokes.

## Why It's Brilliant

Other sports are still fighting over how to credit assists or attribute defensive value. Golf solved this problem cleanly in the 2010s:

- **Course-adjusted** — a birdie on a 550-yard par 5 is worth less than on a 460-yard par 4
- **Decomposable** — you can split total SG into Off-the-Tee, Approach, Around-the-Green, Putting
- **Sample-stable** — ~50 rounds gives you a reliable signal for most components

## Course-Fit Model

I'm building a model that predicts player performance at specific courses using 5-year SG component averages matched against course DNA (width, rough penalty, green firmness, elevation).

Early regression results show **SG: Approach** is the single best predictor of performance at ball-striker courses (Augusta, Muirfield Village), while **SG: Putting** variance matters most at courses with unusual green complexes.

More to come as I get the track records cleaned up.
