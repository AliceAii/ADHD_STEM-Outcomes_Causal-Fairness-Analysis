# ADHD_STEM-Outcomes_Causal-Fairness-Analysis

Causal Fairness Analysis of ADHD Status and High School STEM Outcomes

## Overview

This study applies the Causal Fairness Analysis (CFA) framework (Plecko & Bareinboim, 2024) to decompose the observed disparity in high school STEM GPA and science identity between ADHD-diagnosed and non-ADHD students into confounded, indirect, and direct causal components. Using data from the High School Longitudinal Study of 2009 (HSLS:09), the analysis provides a causal perspective on how a neurodevelopmental health condition translates into educational inequality.

## Research Questions

1. To what extent does ADHD status contribute to disparities in high school STEM outcomes, and through what causal pathways (confounding, indirect, direct) does this disparity operate?
2. How does the total causal effect of ADHD on STEM outcomes vary across student demographic subgroups (race/ethnicity, SES, educational expectations)?
3. To what extent does the direct causal effect of ADHD on STEM outcomes differ across students' demographic backgrounds?

## Causal Model

The analysis follows the Standard Fairness Model (SFM):

- **X (Protected Attribute):** ADHD diagnosis status
- **Z (Confounders):** 9th-grade science identity, race/ethnicity, sex, family SES quintile, educational expectations
- **W (Mediators):** 11th-grade Algebra II, Geometry, and Pre-calculus enrollment; science club participation
- **Y (Outcomes):** High school STEM GPA; 11th-grade science identity

## Methods

| Step | Method | Purpose |
|------|--------|---------|
| Total Variation Decomposition | Semiparametric debiased estimation (`faircause`) | Decompose ADHD–outcome gap into direct, indirect, and confounded effects |
| CATE Estimation | Generalized Random Forest (`grf`) | Estimate heterogeneity in total causal effect across subgroups |
| ctf-DE Estimation | One-step debiased estimator with cross-fitting | Estimate heterogeneity in the direct effect across subgroups |
| Sensitivity Analysis | `sensemakr` + propensity score overlap trimming | Assess robustness to unmeasured confounding and positivity violations |

## Repository Structure
```
├── ADHD_STEM outcomes_hsls.qmd        # Main analysis script (Quarto)
├── r/
│   ├── cnd-effects.R           # Conditional effect estimation functions (Developed by Plecko)
│   └── one-step-debiased.R     # OSD estimator with cross-fitting (XGBoost) (Developed by Plecko)
├── Fig1.SFM.png                # Standard Fairness Model diagram
├── Fig2.tv_decomposition.png   # Total variation decomposition plot
├── Fig3.cate_heatmap.png       # CATE heatmaps by race × education/SES
├── Fig4.cde_heatmap.png        # Direct effect heatmaps by race × education/SES
├── Fig5.overlap_sensitivity.png # Propensity score overlap trimming sensitivity
└── README.md
```

## Requirements

### R Packages
```r
# Data
haven, tidyverse, dplyr, forcats, naniar, mice

# Tables & Visualization
tableone, table1, cobalt, flextable, knitr, ggplot2, patchwork

# Causal Inference
faircause    # devtools::install_github("dplecko/CFA")
grf          # Generalized Random Forest
sensemakr    # Sensitivity analysis
xgboost      # Nuisance parameter estimation

# Utilities
zeallot, data.table, skimr
```

### Data

This study uses restricted-use data from the [High School Longitudinal Study of 2009 (HSLS:09)](https://nces.ed.gov/surveys/hsls09/) administered by the National Center for Education Statistics (NCES). Access requires a restricted-use data license.

## References

- Drago Plečko and Elias Bareinboim (2024), “Causal Fairness Analysis”, *Foundations and Trends in Machine Learning*. Vol. 17, No. 3, pp 1–238. DOI: 10.1561/2200000106.

## Author

Shuhan (Alice) Ai — UCLA