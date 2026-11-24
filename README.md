# E-commerce Website Design, Satisfaction, Trust and Loyalty

A survey analysis in R (Quarto) of how website design features relate to customer satisfaction, trust and loyalty.

## Summary

73 respondents rated an e-commerce website after using it, answering 26 Likert-style questions on a 1-10 scale. The questions group into eight constructs:

| Construct | Items | Role |
|---|---|---|
| Typography | q1-q3 | Design feature |
| Color | q4-q5 | Design feature |
| Content quality | q6-q8 | Design feature |
| Interactivity | q9-q13 | Design feature |
| Navigation | q14-q18 | Design feature |
| Satisfaction | q19-q22 | Outcome |
| Trust | q23-q24 | Outcome |
| Loyalty | q25-q26 | Outcome |

The analysis tests the path **design features → satisfaction → trust → loyalty** and profiles who the respondents are and how they differ.

## Repository contents

| File | Description |
|---|---|
| `Website-satisfaction-survey.qmd` | Quarto report with all analyses (renders to a self-contained HTML file) |
| `dataset.csv` | Survey data: 73 rows x 31 columns (`user_id`, `language`, `platform`, `gender`, `age`, `q1`-`q26`) |

## Analyses

Each chunk is self-contained and follows the same six steps: Library, Data Connection, Data Cleaning, Data Preparation, Analysis, Conclusion.

1. **Descriptive statistics and data quality** – respondent profile, item and construct means, straight-liner check, score distributions.
2. **Scale reliability** – Cronbach's alpha per construct and for the combined design items (benchmark 0.70).
3. **Correlations** – Spearman correlations between constructs with Holm-adjusted p-values and a heatmap.
4. **Group comparisons** – Mann-Whitney tests by platform (Desktop vs Mobile) and gender, plus Spearman correlation of age with each construct.
5. **Regression paths** – standardised linear models: Satisfaction ~ five design features, Trust ~ Satisfaction, Loyalty ~ Satisfaction + Trust, with VIF and residual normality checks.
6. **Exploratory factor analysis** – KMO, Bartlett, parallel analysis and varimax-rotated loadings for the 18 design items, compared against the intended structure.
7. **Respondent segments** – K-Means (k chosen by silhouette width) and Ward hierarchical clustering on construct scores.
8. **Confidence intervals** – t-based and bootstrap CIs for construct means, and the share of respondents with a favourable score (>= 7) with proportion CIs.

## Data cleaning rules

- Duplicate `user_id` rows are dropped.
- Item answers outside 1-10 are set to missing.
- Ages outside 10-100 are set to missing.
- `"null"` platform values are treated as missing.
- Respondents with no valid item answers are removed.
- Construct score = mean of its items.

## Requirements

- R and Quarto
- R packages: `dplyr`, `tidyr`, `ggplot2`, `readr`, `psych`, `car`, `cluster`

## How to run

1. Place `dataset.csv` in the same folder as the `.qmd` file (or change `DATA_PATH` in each chunk).
2. Render: `quarto render Website-satisfaction-survey.qmd`

## Limitations

- Small sample (n = 73): intervals are wide and the factor analysis is exploratory only.
- Few Desktop respondents, so platform comparisons have low power.
- Color, Trust and Loyalty have only two items each, so alpha is less stable.
- Observational data: the regression paths show associations, not causation.
- Design features overlap strongly (check the VIFs), which can mask individual effects.
- Clusters are descriptive groupings of this sample, not validated customer segments.
