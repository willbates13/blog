---
title: "Building a Player Efficiency Model Beyond PER"
date: 2026-05-20
tags: ["NBA", "efficiency", "modeling"]
summary: "PER has been the go-to efficiency stat for decades but it's deeply flawed. Here's how I built a replacement using box score plus-minus and contextual adjustments."
sport: "basketball"
---

## Why PER Falls Short

John Hollinger's Player Efficiency Rating was groundbreaking in 2004. In 2026 it's showing its age. The biggest problems:

- **Pace-independent but team-dependent** — playing on a fast team inflates your raw production
- **No defensive credit** — steals and blocks are rewarded but off-ball defense is invisible
- **Linear weights from the 80s** — the value of a 3PA vs a mid-range FGA has changed dramatically

## The Model

I built a replacement using three inputs:

1. **Regularized Adjusted Plus-Minus (RAPM)** as the ground truth signal
2. **Box score components** as the predictors, with weights fit via ridge regression
3. **Team context adjustment** — correcting for pace, offensive scheme, and usage role

```python
import pandas as pd
from sklearn.linear_model import Ridge

features = [
    'ts_pct', 'ast_pct', 'reb_pct', 'tov_pct',
    'usg_pct', 'blk_pct', 'stl_pct', 'foul_rate'
]

X = player_df[features]
y = player_df['rapm_5yr_prior']

model = Ridge(alpha=1.0)
model.fit(X, y)
```

## Early Results

The model correlates with 5-year RAPM at **r = 0.71** on the holdout set, versus PER's **r = 0.48**. The biggest weight shifts:

| Feature | PER weight | New weight |
|---|---|---|
| True Shooting % | Moderate | **High** |
| Turnover rate | Low | **High** |
| 3PA rate | None | **Moderate** |

Next steps: incorporate tracking data for defensive positioning and add a Bayesian prior for small-sample players.
