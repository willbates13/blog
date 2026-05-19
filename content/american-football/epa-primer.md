---
title: "Expected Points Added: The NFL's Most Useful Model"
date: 2026-05-10
tags: ["NFL", "EPA", "play-by-play"]
summary: "EPA is the backbone of modern NFL analytics. Here's how it works, where it breaks down, and how I'm using it as an input to a play-calling tendency model."
sport: "football"
---

## What EPA Actually Measures

Expected Points Added quantifies the value of each play relative to what was expected before the snap. A 7-yard gain on 3rd-and-6 is worth more EPA than a 12-yard gain on 1st-and-10 because it converts the down.

The expected points model is built from historical play-by-play: given down, distance, and field position, what is the average scoring outcome for the possession?

## Building an EPA-Based Play-Calling Model

I'm fitting a model to predict offensive coordinator tendencies using:

- **Situational EPA by play type** (pass vs run, screen vs deep, etc.)
- **Down/distance splits** — does the OC go conservative or aggressive in obvious passing situations?
- **Game script interaction** — do they abandon the run too early when trailing?

The goal is a "tendency fingerprint" for each OC that updates weekly as game film comes in. This could be useful for defensive game-planning or betting markets.

## Current Limitations

EPA from nflfastR is solid but has known issues:
- Garbage time distorts late-game EPA
- Neutral site and weather adjustments are rough
- Receiver separation isn't captured — a checkdown and a deep shot look the same pre-snap

I'm working on corrections for the first two; the tracking data gap is harder to fill.
