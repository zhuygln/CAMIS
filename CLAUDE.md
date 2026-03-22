# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

CAMIS (Comparing Analysis Method Implementations in Software) is a Quarto-based static website that documents and compares statistical method implementations across R, SAS, and Python. It is a cross-industry PHUSE Working Group collaboration published at https://psiaims.github.io/CAMIS/.

## Build Commands

```bash
# Render the full site (runs pre-render dependency check automatically)
quarto render

# Render a single page
quarto render path/to/file.qmd

# Preview site locally with live reload
quarto preview
```

There is no test suite or linter. CI validates that `quarto render` succeeds.

## Environment Setup

```bash
# R dependencies (managed by renv, R 4.5.2)
# In R console:
renv::restore()

# Python dependencies (Python 3.12, virtualenv managed by renv)
pip install -r requirements.txt
```

The renv virtualenv lives at `./renv/python/virtualenvs/renv-python-3.12`. R packages are locked in `renv.lock`. Python packages are locked in `requirements.txt`.

## Architecture

**Content organization by language and method:**
- `R/` — R implementations as `.qmd` files (50+ methods)
- `SAS/` — SAS implementations
- `python/` — Python implementations (scipy, statsmodels, etc.)
- `Comp/` — Cross-language comparison files (e.g., R vs SAS vs Python)

**Supporting directories:**
- `data/` — Datasets (CSV, RData, SAS .sas7bdat) used in examples
- `images/` — Organized by method category (survival, logistic_regression, etc.)
- `templates/` — `single_language_template.qmd` and `multi_language_template.qmd` for new pages
- `utils/` — Build utilities including `quarto_check_pkg_dependencies.R`
- `_freeze/` — Quarto execution cache (auto-generated, do not edit)

**Key configuration:**
- `_quarto.yml` — Quarto project config: website type, Cosmo theme, navbar structure, `freeze: auto`
- `renv.lock` — R dependency lockfile
- `.Renviron` / `.Rprofile` — R environment setup (loads renv automatically)

## How the Build Works

Quarto's `freeze: auto` caches code execution results in `_freeze/`. A pre-render script (`utils/quarto_check_pkg_dependencies.R`) compares current R and Python package versions against `data/quarto_pkg_dependencies.csv` and invalidates cached files when dependencies change. This means most renders only re-execute pages with changed content or dependencies.

## Content Conventions

- Each statistical method gets its own `.qmd` file in the appropriate language directory
- New pages should follow the templates in `templates/`
- The method index is tracked in `data/stat_method_tbl.csv`
- When adding a new R package dependency, it must be added to the renv lockfile (`renv::snapshot()`)
- Python package additions go in `requirements.txt`

## CI/CD

GitHub Actions (`.github/workflows/action.yml`) renders on push to main and deploys to gh-pages. PR builds (`.github/workflows/pull_request_action.yml`) generate preview deployments. Both workflows install system deps (libcurl, gdal, libudunits2), set up R with renv, and install Python packages before rendering.
