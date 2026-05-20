# WIC Synthetic Analysis

**Regression Discontinuity Evaluation of WIC Program Effects on Infant Birth Weight**

Colin Heeneman, Emily Frost, Samantha Sepulveda
PA 528 · Dr. Siciliano · December 2024 · Updated April 2026

---

## Findings

This analysis uses a Regression Discontinuity Design (RDD) to estimate the causal effect of WIC participation on infant birth weight, exploiting the program's income eligibility threshold as a natural experiment. Results are reported across two synthetic scenarios to assess sensitivity to data-generating assumptions.

**Optimistic scenario:** WIC participation is associated with a **257.9-gram increase in birth weight** (95% CI: 131.1 to 384.8; z = 3.99, p < 0.001) for mothers near the income eligibility threshold. The effect is statistically significant and robust across alternative bandwidth specifications.

**Pessimistic scenario:** The estimated effect is **87.4 grams** (95% CI: -54.3 to 229.1; z = 1.21, p = 0.227). The effect is positive in direction but not statistically significant, suggesting the program's impact may be modest or sensitive to implementation quality and participant compliance.

Across both scenarios, density diagnostics find no evidence of income manipulation near the eligibility threshold, supporting the core identifying assumption of the RDD.

---

## Project Overview

The Special Supplemental Nutrition Program for Women, Infants, and Children (WIC) serves low-income pregnant women, new mothers, and young children by providing supplemental foods, nutrition education, and healthcare referrals. As of 2024, WIC reaches approximately 53% of all infants born in the United States.

This analysis evaluates WIC's effect on infant birth weight using a sharp RDD centered on the program's income eligibility cutoff. Individuals just below and just above the threshold are treated as locally comparable, enabling causal inference without randomization. Because WIC enrollment is determined by an income threshold, the design isolates program effects from the broader socioeconomic determinants of health.

### Why Synthetic Data

This analysis uses synthetic data by deliberate methodological choice, not as a limitation. Administrative WIC records are not publicly available at the individual level due to confidentiality protections, and constructing a valid natural experiment with publicly available birth weight microdata was outside the scope of this project. The synthetic approach allows the analysis to demonstrate the full RDD workflow (identification strategy, bandwidth selection, manipulation testing, robustness checks) under controlled and transparent data-generating assumptions.

Two scenarios are simulated in parallel: an optimistic specification with stronger assumed program effects and a pessimistic specification with more conservative assumptions. This dual-scenario design makes the sensitivity of estimates to underlying assumptions explicit rather than hidden.

---

## Methods

- **Design:** Sharp Regression Discontinuity
- **Running variable:** Household income (as a percentile of the eligibility threshold)
- **Cutoff:** Income threshold at the 25th percentile of the simulated distribution
- **Outcome:** Infant birth weight in grams
- **Estimator:** `rdrobust` with mean-squared-error optimal bandwidth selection (Calonico, Cattaneo, Titiunik 2014)
- **Robustness:** Bandwidth sensitivity analysis across three specifications per scenario; McCrary density test for manipulation
- **Covariates:** Maternal race, pre-existing health conditions, maternal nutrition index, healthcare access index, maternal age

---

## Repository Structure

```
WIC-Synthetic-Analysis/
├── WIC NO CODE.qmd              # Primary analysis document (Quarto, code folded)
├── WIC NO CODE.html             # Rendered HTML output
├── WIC-NO-CODE.pdf              # PDF output (code hidden)
├── WIC-code-displayed.pdf       # PDF output (code visible)
├── Simulation.qmd               # Synthetic data generation scripts
├── simulated_wic_data_optimistic.csv    # Optimistic scenario dataset (n = 1,000)
├── simulated_wic_data_pessimistic.csv   # Pessimistic scenario dataset (n = 1,000)
├── simulated_wic_data.csv               # Combined dataset
├── simulated_wic_data_updated.csv       # Revised combined dataset
├── wic-styles.css               # Custom CSS for HTML output
├── renv.lock                    # Package lockfile for reproducibility
└── WIC.Rproj                    # RStudio project file
```

---

## Reproducing the Analysis

This project uses [renv](https://rstudio.github.io/renv/) for package management and [Quarto](https://quarto.org) for document rendering.

**1. Clone the repository**

```bash
git clone https://github.com/colinheeneman/WIC-Synthetic-Analysis.git
cd WIC-Synthetic-Analysis
```

**2. Restore the R environment**

Open the project in RStudio (via `WIC.Rproj`) or launch R in the project directory, then run:

```r
renv::restore()
```

**3. Regenerate synthetic data (optional)**

To regenerate the simulated datasets from scratch, render `Simulation.qmd`:

```bash
quarto render Simulation.qmd
```

**4. Render the analysis**

```bash
quarto render "WIC NO CODE.qmd"
```

This produces `WIC NO CODE.html` with code folded and `WIC-NO-CODE.pdf`.

---

## Key Packages

| Package | Purpose |
|---|---|
| `rdrobust` | RDD estimation and inference |
| `rddensity` | McCrary manipulation test |
| `ggplot2` | Visualization |
| `gt` | Summary tables |
| `showtext` | EB Garamond typography in figures |
| `dplyr` | Data manipulation |

---

## Authors

**Colin Heeneman** · MPP, University of Illinois Chicago
[colin-heeneman.github.io](https://colin-heeneman.github.io)

**Emily Frost** · MPP, University of Illinois Chicago

**Samantha Sepulveda** · MPP, University of Illinois Chicago

---

*Completed December 2024 as part of PA 528 (Program Evaluation) at UIC's School of Public Policy and Administration. Updated April 2026.*
