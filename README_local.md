# README_local.md

A local guide to the CAMIS repository — what's inside, how it's organized, and where to find cross-language benchmarks.

## What Is CAMIS?

CAMIS (Comparing Analysis Method Implementations in Software) is a Quarto-rendered static website that documents how statistical methods are implemented in **R**, **SAS**, and **Python**, and — critically — where those implementations **agree or disagree**. It is maintained by a cross-industry PHUSE Working Group (pharmaceutical/regulatory). The live site is at <https://psiaims.github.io/CAMIS/>.

---

## Repository Layout

| Path | What's there |
|---|---|
| `R/` | 54 Quarto (`.qmd`) files, each implementing a statistical method in R |
| `SAS/` | 45 `.qmd` files doing the same in SAS |
| `python/` | 16 `.qmd` files doing the same in Python (scipy, statsmodels, etc.) |
| `Comp/` | **38 comparison files** — the "apple-to-apple" benchmarks (see next section) |
| `East/` | 1 file: group sequential design for time-to-event using Cytel EAST software |
| `data/` | Shared datasets (CSV, RData, SAS .sas7bdat) used across all implementations |
| `images/` | Figures organized by method (e.g. `images/survival/`, `images/logistic_regression/`) |
| `templates/` | `single_language_template.qmd` and `multi_language_template.qmd` — starter files for new pages |
| `method_summary/` | Introductory/overview pages for CIs for proportions, sample size theory, ML methods |
| `utils/` | Build utilities — notably `quarto_check_pkg_dependencies.R` (cache invalidation) |
| `contribution/` | How to contribute, environment setup guide, R package review process |
| `publication/` | White paper, conference presentations, dissertation project links |
| `blogs/` | Blog index (conference highlights, technical posts) |
| `minutes/` | Meeting minutes archive with annual team member lists |
| `non_website_content/` | Archived/older material (past conference pages, hackathon notes) |
| `_freeze/` | Quarto execution cache — auto-generated, do not edit |
| `renv/`, `renv.lock` | R package environment (R 4.5.2, 150+ packages) |
| `requirements.txt` | Python package list (126 packages, Python 3.12) |
| `_quarto.yml` | Site configuration (Cosmo theme, navbar, freeze settings) |
| `data/stat_method_tbl.csv` | **Master index** of all 67 methods with links to each language's page and comparison |

---

## Cross-Language Comparisons (the Benchmarks You Want)

All comparison files live in `Comp/`. Each runs the **same analysis on the same data** in multiple languages and documents whether results match, and explains any discrepancies.

### Three-Language Comparisons (R + SAS + Python)

Only **one** method currently has a full R vs SAS vs Python comparison:

| Method | File |
|---|---|
| Survey statistics (means, totals, ratios, proportions, quantiles, domain analysis) | `Comp/r-sas-python_survey-stats-summary.qmd` |

### Methods with R, SAS, AND Python Implementations (but R-vs-SAS comparison only)

These methods have standalone pages in all three languages, so the code exists to compare across all three, but the formal `Comp/` file only compares R vs SAS. You can use the individual language pages to do your own three-way comparison:

| Method | R page | SAS page | Python page | Comparison |
|---|---|---|---|---|
| Rounding | `R/rounding` | `SAS/rounding` | `python/Rounding` | `Comp/r-sas_rounding` |
| Summary statistics | `R/summary-stats` | `SAS/summary-stats` | `python/Summary_statistics` | `Comp/r-sas-summary-stats` |
| Skewness/Kurtosis | `R/summary_skew_kurt` | `SAS/summary_skew_kurt` | `python/skewness_kurtosis` | `Comp/r-sas_summary_skew_kurt` |
| One-sample t-test | `R/ttest_1Sample` | `SAS/ttest_1Sample` | `python/one_sample_t_test` | `Comp/r-sas_ttest_1Sample` |
| Paired t-test | `R/ttest_Paired` | `SAS/ttest_Paired` | `python/paired_t_test` | `Comp/r-sas_ttest_Paired` |
| Two-sample t-test | `R/ttest_2Sample` | `SAS/ttest_2Sample` | `python/two_samples_t_test` | `Comp/r-sas_ttest_2Sample` |
| ANOVA | `R/anova` | `SAS/anova` | `python/anova` | `Comp/r-sas_anova` |
| ANCOVA | `R/ancova` | `SAS/ancova` | `python/ancova` | `Comp/r-sas_ancova` |
| MANOVA | `R/manova` | `SAS/manova` | `python/MANOVA` | `Comp/r-sas_manova` |
| Linear regression | `R/linear-regression` | `SAS/linear-regression` | `python/linear_regression` | `Comp/r-sas_linear-regression` |
| Logistic regression | `R/logistic_regr` | `SAS/logistic-regr` | `python/logistic_regression` | `Comp/r-sas_logistic-regr` |
| Kruskal-Wallis | `R/kruskal_wallis` | `SAS/kruskal_wallis` | `python/kruskal_wallis` | `Comp/r-sas_kruskalwallis` |
| Chi-square / Fisher's exact | `R/association` | `SAS/association` | `python/chi-square` | `Comp/r-sas_chi-sq` |
| Correlation (Pearson/Spearman/Kendall) | `R/correlation` | `SAS/correlation` | `python/correlation` | `Comp/r-sas_correlation` |

### R vs SAS Only Comparisons

These have comparison files but **no Python implementation** yet:

| Category | Method | File |
|---|---|---|
| **GLM** | Negative binomial regression | `Comp/r-sas_negbin.qmd` |
| **Non-parametric** | Wilcoxon signed-rank test | `Comp/r-sas-wilcoxonsr_HL.qmd` |
| **Non-parametric** | Mann-Whitney / Wilcoxon rank-sum | `Comp/r-sas-wilcoxon-ranksum_hl.qmd` |
| **Non-parametric** | Friedman test | `Comp/r-sas_friedman.qmd` |
| **Non-parametric** | Jonckheere-Terpstra test | `Comp/r-sas_jonckheere.qmd` |
| **Categorical** | McNemar's test | `Comp/r-sas_mcnemar.qmd` |
| **Categorical** | Cochran-Mantel-Haenszel | `Comp/r-sas_cmh.qmd` |
| **Categorical** | CIs for single proportion | `Comp/r-sas_ci_for_prop.qmd` |
| **Mixed models** | Random effects (LMM) | `Comp/r-sas_random_effects_models.qmd` |
| **Mixed models** | MMRM | `Comp/r-sas_mmrm.qmd` |
| **Mixed models** | GLMM | `Comp/r-sas_glmm.qmd` |
| **Mixed models** | GEE | `Comp/r-sas_gee.qmd` |
| **Missing data** | Tipping point analysis | `Comp/r-sas_tipping_point.qmd` |
| **Missing data** | Reference-based MI (joint model) | `Comp/r-sas_rbmi_continuous_joint.qmd` |
| **Survival** | Kaplan-Meier / log-rank / Cox PH | `Comp/r-sas_survival.qmd` |
| **Survival** | Cause-specific hazards | `Comp/r-sas_survival_csh.qmd` |
| **Survival** | Cumulative incidence functions | `Comp/r-sas_survival_cif.qmd` |
| **Survival** | Recurrent events (AG, LWYY, PWP) | `Comp/r-sas_recurrent_events.qmd` |
| **Survival** | Tobit regression | `Comp/r-sas_tobit.qmd` |
| **Causal** | Propensity score matching | `Comp/r-sas_psmatch.qmd` |
| **Causal** | Propensity score weighting | `Comp/r-sas_psweight.qmd` |
| **Sample size** | Superiority studies | `Comp/r-sas_s_size_sup.qmd` |
| **Sample size** | Group sequential design (TTE) | `Comp/r-east_gsd_tte.qmd` (R vs SAS vs EAST) |

### Python-Only Pages (no SAS, no formal comparison)

These Python implementations exist without a corresponding comparison file:

- `python/binomial_test.qmd` — Single proportion binomial test (R and SAS pages exist but no comparison file)

---

## Shared Datasets

All implementations pull from `data/`. Key datasets:

| File | Used for |
|---|---|
| `adcibc.csv` / `adcibc.Rdata` | Clinical trial data — ANCOVA, MMRM, mixed models, multiple imputation |
| `blood_pressure.csv` | Paired t-test, non-parametric tests |
| `blood_pressure_ties.csv` | Wilcoxon tests with ties handling |
| `drug_trial.csv` | GEE, generalized models |
| `lung_cancer.csv` / `NCCTG_Lung_Cancer_Data_535_29.csv` | Survival analysis (Kaplan-Meier, Cox, competing risks) |
| `bmt.sas7bdat` / `whas500.sas7bdat` | SAS-format survival data |
| `htwt.csv` | Linear regression |
| `manova1.csv` | MANOVA |
| `polyps.csv` | Count data / negative binomial regression |
| `colds.csv` | Non-parametric analysis |
| `jonck.csv` | Jonckheere-Terpstra test |
| `ps_data.csv` | Propensity score matching/weighting |
| `nhanes.csv` / `apisrs.csv` | Survey statistics |
| `Mall_Customers.csv` | Clustering, PCA |
| `trial01.csv` | Sample size calculations |
| `sas_disease.csv` | Categorical analysis |
| `resp_gee.xlsx` | GEE respiratory data |
| `stat_method_tbl.csv` | Master method index (not analysis data — used to build the website's method table) |
| `quarto_pkg_dependencies.csv` | Build system cache tracking (auto-generated) |

---

## How to Use This as a Benchmark

**If you want to verify that your Python/R/SAS code produces correct results:**

1. **Pick a method** from `data/stat_method_tbl.csv` or the tables above.
2. **Find the shared dataset** — each language implementation uses the same CSV/data from `data/`.
3. **Read the individual language pages** in `R/`, `SAS/`, `python/` to see the exact code and output.
4. **Read the comparison page** in `Comp/` to see where results match and where they diverge, and *why*.

**The strongest three-way benchmarks** are the 14 methods listed in the "Methods with R, SAS, AND Python Implementations" table above. These give you runnable code in all three languages on the same data, plus a formal R-vs-SAS comparison that documents expected outputs.

**For the richest comparison detail**, look at the `Comp/` files — they typically include side-by-side output tables showing exact numeric results, call out rounding/algorithm differences, and explain which parameter settings are needed to get matching results across tools.

---

## Methods with No Implementation Yet

The method index (`data/stat_method_tbl.csv`) tracks several methods that are planned but have no code yet:

- CIs for two paired proportions
- CIs for proportions in stratified designs
- CIs for Poisson exposure-adjusted incidence rates
- Bayesian repeated measures MMRM
- Group sequential designs for binary endpoints
- Lasso and Ridge regression

---

## Key Configuration Files

| File | Purpose |
|---|---|
| `_quarto.yml` | Quarto project config — site type, navbar, Cosmo theme, `freeze: auto` |
| `renv.lock` | R dependency lockfile (150+ packages pinned) |
| `requirements.txt` | Python dependencies (126 packages) |
| `.Renviron` | R environment vars (renv settings, Posit Package Manager) |
| `.Rprofile` | Auto-loads renv on R startup |
| `camis.Rproj` | RStudio project file |
| `.github/workflows/action.yml` | CI: renders site on push to main, deploys to gh-pages |
| `.github/workflows/pull_request_action.yml` | CI: builds PR previews |

---

## Building / Rendering

```bash
# Full site render (pre-render script checks dependency changes automatically)
quarto render

# Single page
quarto render R/anova.qmd

# Local preview with live reload
quarto preview
```

R dependencies: restore with `renv::restore()` in an R console.
Python dependencies: `pip install -r requirements.txt` (or use the renv-managed virtualenv).
