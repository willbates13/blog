---
title: "Expected Goals in Hockey: Building xG from Shot Data"
date: 2026-05-05
tags: ["NHL", "xG", "expected goals", "modeling"]
summary: "Expected goals models have transformed hockey analytics. Here's how to build a basic xG model from publicly available shot data and what its limitations are."
sport: "hockey"
---

## Why xG Over Corsi

Corsi (shot attempts for/against) was a revolutionary stat when it emerged from the hockey blogosphere in the late 2000s. It established that puck possession predicts outcomes better than traditional +/-. But it treats a shot from the slot the same as a shot from the boards.

Expected goals weights each shot by the probability it becomes a goal, using:

- **Shot location** (distance + angle)
- **Shot type** (wrist, snap, slap, deflection, tip)
- **Game state** (5v5, power play, etc.)
- **Rebound** (shots within a few seconds of a prior shot are much more dangerous)

## The Model

Using publicly scraped NHL play-by-play data:

```python
from sklearn.ensemble import GradientBoostingClassifier

features = ['shot_distance', 'shot_angle', 'is_rebound',
            'shot_type_encoded', 'strength_state']

X = shots[features]
y = shots['is_goal']

xg_model = GradientBoostingClassifier(n_estimators=200, max_depth=4)
xg_model.fit(X_train, y_train)
```

AUC on the holdout set: **0.77** — reasonable for this feature set.

## What xG Doesn't Capture

- Goaltender quality (a Vezina-caliber goalie saves shots xG says should go in)
- Pre-shot movement and passing sequences
- Traffic in front of the net

The next iteration adds a goalie adjustment layer and tries to incorporate zone-entry data as a leading indicator.
