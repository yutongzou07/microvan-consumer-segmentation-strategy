# microvan-consumer-segmentation-strategy
# Microvan Concept: Consumer Segmentation & Positioning Strategy

**Market intelligence case analysis** — factor analysis, regression, and cluster segmentation to identify the target market and positioning strategy for a new "microvan" concept vehicle.

*Team project (Team 33): Abby Chen, Chloe Hu, Evelyn Wang, Vedansh Sharma, Yutong Zou*

[Open in Colab](https://colab.research.google.com/github/yutongzou07/microvan-consumer-segmentation-strategy/blob/main/Microvan_Case_Team_33_Pt4_Done_(1).ipynb)

## Business Problem

A vehicle manufacturer is evaluating a new "microvan" concept — positioned between a compact car and a traditional minivan — and needs to determine **who** the target consumer is and **how** to position the vehicle in market, based on a consumer survey measuring liking (`mvliking`) against 30 vehicle attribute ratings and respondent demographics.

## Approach

**1. Baseline regression**
Regressed concept liking against all 30 raw attribute variables. The model was statistically significant overall (F-stat p < 0.001, R² = 0.373), but severe multicollinearity meant most individual attributes weren't independently significant — the raw attributes couldn't isolate real drivers of preference.

**2. Factor analysis**
Ran Principal Component Analysis with Varimax rotation (validated with Bartlett's Test of Sphericity, p < 0.001, and KMO = 0.923) to reduce the 30 attributes into **5 interpretable factors**: Luxury, Compact Utility, Family, Green, and Safety.

**3. Factor-based regression**
Re-ran the regression using the 5 factor scores instead of raw attributes. This traded a small amount of explanatory power (R² dropped from 0.373 to 0.337) for a far more interpretable model, isolating **Luxury** and **Compact Utility** as the strongest positive predictors of liking (coefficients of 1.09 and 1.03, both p < 0.001), while **Safety** was a significant *negative* predictor (coefficient of -0.59, p < 0.001). Family and Green factors were not statistically significant.

**4. Segmentation**
Used hierarchical clustering (Ward's method) on the 5 factor scores to determine cluster count, confirmed with K-means (k=3), then profiled each segment on demographics (age, income, education, number of children) and validated differences in concept liking with a one-way ANOVA (F = 44.29, p < 0.001).

## Key Findings — Segments

| Segment | Profile | Mean Concept Liking |
|---|---|---|
| **Affluent Family-Oriented Buyers** | Middle-aged (44), high income (~$83K), most children, highest education | **6.60 (highest)** |
| **Affluent Established Traditionalists** | Oldest (46), highest income (~$104K), fewer/older children | 4.42 (moderate) |
| **Young Budget-Conscious Non-Family Consumers** | Youngest (32), lowest income (~$37K), fewest children | 3.89 (lowest) |

The segment with the strongest functional need for a family-capable-but-compact vehicle showed by far the highest concept liking — demographics aligned closely with the psychological drivers (Luxury, Compact Utility) identified in the factor analysis.

## Recommendation

**Target the Affluent Family-Oriented segment.** Position the microvan as an upscale, compact, and versatile vehicle for urban/suburban family life — emphasizing premium interior quality, smart design, and ease of use. Present safety as a reassuring baseline rather than a lead message, since safety-focused consumers were, counterintuitively, less receptive to the concept overall. Avoid targeting segments defined by traditional or budget vehicle preferences, which showed structurally lower interest regardless of messaging.

## Tools

Python — pandas, statsmodels (OLS regression), factor_analyzer (PCA with Varimax rotation), scipy (hierarchical clustering), scikit-learn (K-means), one-way ANOVA

## Notes

This was a team project completed for Duke Fuqua's MQM program. Survey data is not included in this repository per course policy; this repo contains only the analysis write-up and code contributions.
