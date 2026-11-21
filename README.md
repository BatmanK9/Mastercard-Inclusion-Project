# Mastercard-Inclusion-Project

# Inclusive Growth in the Lower Ninth Ward

**Data Science final project · Dillard University · November 2026**
Team: Kedrick Carter, Kedrick Gutter, [add any other teammate]

## Research question

How does the Lower Ninth Ward compare to the rest of Orleans Parish in Inclusive Growth, and which factors are most responsible for the disparity?

## Headline results

| Finding | Result |
|---|---|
| 2025 gap | Lower 9th export averages **35.7** vs **42.6** for the rest of Orleans (**−6.9 points**) |
| Persistence | Lower in **9 of 9 years** (2017–2025); one-sided Mann-Whitney p ≈ 0.00001 |
| Spread | 82% of Lower 9th tracts score below the rest-of-Orleans median (35.0 vs 42.0); tract range 23–54 |
| By pillar (share of gap) | Place 43%, Economy 31%, Community 26% |
| Largest indicator shortfalls | Labor Market Engagement −1.28, Acres of Park Land −1.25, Spending per Capita −0.80, Commercial Diversity −0.80, Internet Access −0.63 points (together 69% of the gap) |
| Forecast (2026) | Gap of about −6.0; read as a gap of 6–7 points that is not forecast to close |
| Model accuracy | Typical error 2.9 points vs 3.2 for "no change" |
| Fairness check | The model runs too high for the Lower 9th (+2.2 points on average vs +1.2 for the rest of Orleans) |

## Repository contents

```
├── IGS_Lower9th_Phase2_and_Phase3.ipynb   # the full analysis (run this one)
├── data/
│   ├── Inclusive_Growth_Score_Data_Export_20-11-2026_181802_Compared_to_Urban-Rural.csv   # Lower 9th export
│   └── Inclusive_Growth_Score_Data_Export_20-11-2026_185758Compared_to_Urban-Rural.csv    # New Orleans export
├── outputs/                               # result tables written by the notebook
│   ├── phase3_model_metrics.csv
│   ├── phase3_forecast_2026.csv
│   └── phase3_gap_decomposition.csv
├── docs/
│   └── Phase1_Proposal, Phase3_Model_Evaluation_Report, Executive_Briefing slides
└── README.md
```

The notebook contains all three analysis phases:

- **Part 1, Phase II: cleaning and exploratory analysis.** Rebuilds the two-row header, builds the groups, and tests the gap (7 figures).
- **Part 2, Phase III: forecasting.** Predicts each tract's next-year score and checks the model for fairness (5 figures).
- **Part 3: gap decomposition.** Splits the 2025 gap across the 3 pillars and 18 indicators (2 figures, robustness checks).

## How to run

1. Open `IGS_Lower9th_Phase2_and_Phase3.ipynb(1)` in Google Colab (or Jupyter).
2. Upload the two raw CSVs from `data/` next to the notebook, or into a `raw/` or `data/` folder.
3. Run all cells. The notebook finds the two files by itself and writes the cleaned data and result tables.

Requirements: Python 3, pandas, numpy, scipy, scikit-learn, matplotlib. All are preinstalled in Colab.

## Data

Mastercard Inclusive Growth Score (IGS) exports, downloaded 20 Nov 2026.

- Tract-level scores from 0 to 100, 2017–2025, 207 tracts. Two tracts without scores are dropped.
- 18 indicators grouped into three pillars: Place, Economy, Community.
- Groups: **Lower 9th export** (the 33 scored tracts the dashboard returns for the Lower Ninth Ward, one of which is in St. Bernard Parish), **Rest of Orleans** (149 tracts), and tracts outside Orleans Parish.

## Method summary

- **Cleaning:** missing values are left missing at load time, then imputed (indicators only, never the score) inside cross-validation folds so no information leaks.
- **Forecasting:** Ridge regression on the 18 indicators plus the current score predicts next-year score. Trained on targets through 2022, tested on 2023–2025. Compared against persistence ("no change"), a training-mean baseline and gradient boosting.
- **Fairness check:** prediction bias and error reported separately for the Lower 9th export, the rest of Orleans and tracts outside Orleans.
- **Gap decomposition:** an Oaxaca-Blinder-style regression splits the 2025 gap across indicators, with 95% tract-level bootstrap intervals. A direct pillar split is the headline for pillar-level claims.
- **Validation choices:** tract-grouped cross-validation, cluster bootstrap by tract.

## Limitations

- Results are associations in tract-level scores, not proven causes. The data has no flood, disinvestment or population measures.
- The study area is what the score dashboard returns for the Lower Ninth Ward, not an official boundary.
- The forecast beats "no change" by only about 0.3 points, and not clearly for tracts the model has not seen.
- Because the score is built from the indicators, the decomposition explains almost all of the gap by construction. The useful result is how the gap is divided.

## Team 

| Name |
|---|---|---|
| Kedrick Carter |
| Kedrick Gutter |



## Data source

Mastercard Inclusive Growth Score. Scores and indicator values are as exported from the score dashboard.
