# The Effect of Collaboration on Charting Probability and Chart Rank
### An Analysis of the Billboard Music Top 100 Charts from 2003–2023

> Originally submitted to Course Instructor Victoria Chui for INF1340H – Programming for Data Science, an elective course under the Faculty of Information, University of Toronto.

## Overview

This project investigates whether featuring another artist on a song is associated with better performance on the Billboard Year-End Top 100 charts — specifically, whether it correlates with a better chart rank.

## Data

- Source: [Top 100 Songs & Lyrics From 1959–2019](https://www.kaggle.com/datasets/brianblakely/top-100-songs-and-lyrics-from-1959-to-2019) (Kaggle, Brian Blakely)
- Filtered to 2003–2023
- Columns used: `Year`, `Song Title`, `Artist`, `Rank`, `Featured Artists`

## Method

1. **Cleaning** — parsed the `Featured Artists` field into a binary flag and separated featured-artist names out of the `Artist` field.
2. **Dominant artist analysis** — identified the most-charting artist per year and compared their featured vs. solo song counts and ranks.
3. **Statistical test** — two-sample t-test comparing mean rank of featured vs. solo songs across all 20 years.
4. **Regression** — linear regression predicting `Rank` from `Featured Artists` status.

## Key Findings

| Group | Mean Rank | Median | Std Dev | Count |
|---|---|---|---|---|
| No Feature | 51.16 | 52 | 28.88 | 1525 |
| With Feature | 48.75 | 48 | 28.80 | 575 |

- Featured songs averaged a rank ~2.4 spots better than solo songs.
- Welch's t-test: t = 1.71, **p = 0.088** — not statistically significant at α = 0.05.
- Linear regression MSE ≈ 872 (RMSE ≈ 30) — `Featured Artists` alone has very weak predictive power for rank.

**Conclusion:** There is a small, directionally favorable trend toward featured songs ranking higher, but it is not statistically significant given the sample and variance. The data does not support a claim that collaboration meaningfully improves — let alone causes — a better chart rank.

## Limitations

- Only one predictor (`Featured Artists`) is used; chart rank is influenced by many other factors (genre, artist popularity, streaming trends, etc.) not captured here.
- No reliable data on songs that failed to chart, so "charting probability" could not be modeled with real data and was excluded from the final analysis.
- Dataset does not extend past 2019 lyrics coverage in its original form; chart data for 2020–2023 relies on the same source's chart-only records.

## Repository Structure

```
├── README.md
├── requirements.txt
├── data/
│   └── all_songs_data.csv
├── notebooks/
│   └── analysis.ipynb
└── images/
    └── *.png
```

## Setup

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
pip install -r requirements.txt
jupyter notebook notebooks/analysis.ipynb
```

## Requirements

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- scipy
