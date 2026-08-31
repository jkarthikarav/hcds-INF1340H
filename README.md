# The Effect of Collaboration on Charting Probability and Chart Rank
### An Analysis of the Billboard Music Top 100 Charts from 2003–2023

> Originally submitted to Course Instructor Victoria Chui for INF1340H – Programming for Data Science, a Human-Centered Data Science course under the Faculty of Information, University of Toronto.

## Overview

Charting (i.e., making an appearance on the Billboard Top 100 music charts in the USA) is a highly sought outcome for musicians and their record labels. Some musicians' careers are boosted by their charting prowess, and the more songs on the chart, the more successful an artist's album is deemed to be by critics and fans alike. While such a feat depends on multiple factors, this project asks whether collaboration in the song production process has any effect on a song's chart rank.

Correlation does not imply causation — but people are prone to repeating what looks like it works, whether or not it's the actual cause of the result. The real value of this project isn't proving that collaboration causes a better rank; it's using the data to see whether the pattern even holds up, so that collaboration can be looked at as a data-driven business decision rather than a purely creative one.

## Research Question

Does collaboration affect the chart rank of a song?

## Data

- Source: [Top 100 Songs & Lyrics From 1959–2023](https://www.kaggle.com/datasets/brianblakely/top-100-songs-and-lyrics-from-1959-to-2019) (Kaggle, Brian Blakely)
- Filtered to 2003–2023
- Columns used: Year, Song Title, Artist, Rank, Featured Artists
- The Featured Artists column originally stored a URL/dict of artist image data rather than a usable flag, and the Artist field bundled the featured artist into the name (e.g., "Beyonce feat. Jay-Z"). Both were cleaned into a single boolean: solo (0) or collaborative (1).

## Method

1. **Cleaning** — parsed the `Featured Artists` field into a binary flag and separated featured-artist names out of the `Artist` field.
2. **Dominant artist analysis** — identified the most-charting artist per year and compared their featured vs. solo song counts and ranks.
3. **Statistical test** — two-sample t-test comparing mean rank of featured vs. solo songs across all 20 years.
4. **Regression** — linear regression predicting `Rank` from `Featured Artists` status.

## Key Findings

**Dominant artists don't need collaboration to chart repeatedly.**

Does collaboration at least help rank? Across all 20 years:
| Group | Mean Rank | Median | Std Dev | Count |
|---|---|---|---|---|
| No Feature | 51.16 | 52 | 28.88 | 1525 |
| With Feature | 48.75 | 48 | 28.80 | 575 |

- Featured songs averaged a rank ~2.4 spots better than solo songs.
- Welch's t-test: t = 1.71, **p = 0.088** — not statistically significant at α = 0.05.
- Linear regression MSE ≈ 872 (RMSE ≈ 30) — `Featured Artists` alone has very weak predictive power for rank.

Featured songs average a rank about 2.4 spots better than solo songs. That's the direction you'd expect if collaborating helped — but a Welch's t-test on that gap comes back at t = 1.71, p = 0.088, which doesn't clear the standard 0.05 bar for significance. In other words, that 2–3 spot edge is small enough that it could just be noise rather than a real effect.

The regression tells us the same: predicting Rank from Featured Artists alone gives an MSE of about 872 — meaning the model is off by around 30 ranks, so a 2-rank difference in its predictions (51 without a feature vs. 49 with one) isn't something you can depend upon.

**Conclusion:** 

Collaboration doesn't appear to meaningfully move the needle. Dominant artists chart repeatedly with or without features, and the small edge featured songs show in average rank isn't statistically significant. 

Artists may still choose to collaborate for creative or promotional reasons; but the data doesn't support collaborating for the sake of a better rank.

## Repository Structure

```
├── README.md
├── requirements.txt
├── archive.zip [contains the .csv files, the files are all above 25mb each so i had to upload the zip instead]
├── notebooks/
    └── analysis.ipynb
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
- scikit-learn
- scipy
