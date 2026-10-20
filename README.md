# Mortality Trend Models: Cardiovascular Disease and Cancer in Mexico (1998-2024)

R code for the regression analysis submitted to LKE 2026 (BUAP), revised version.

## Contents

- `Esperanza_de_Vida.Rmd` — main analysis pipeline:
  1. WHO Global Health Observatory data download (NCDMORT3070)
  2. INEGI death-registry aggregation (DuckDB)
  3. CONAPO population data and rate computation
  4. Linear regression (rate ~ year + pandemic indicator)
  5. Pre-pandemic vs. 2020-2024 models
  6. Quasibinomial logistic regression (cause of death ~ period + sex + age group)
- `analisis_revision_LKE.R` — additional checks added in the revision
  (run after the .Rmd, which produces the base tables in `data/`; outputs go to
  `data/revision/`): ICD-10 definitions and year-assignment checks,
  serial-dependence diagnostics (Durbin-Watson, Ljung-Box), alternative
  specifications (Newey-West HAC, AR(1), quadratic trend), sensitivity to the
  pandemic window, and summary counts of the aggregated logistic model.

## Data

Raw source files are not included in this repository due to size
(the INEGI microdata file is ~7 GB). To reproduce the analysis, place
the following files in `data/raw/`:

- `base_defunciones_inegi_1990_2024.csv` — INEGI, Estadisticas de
  Defunciones Registradas (EDR), obtained via INSP.
- `0_Pob_Mitad_1950_2070.xlsx` — CONAPO, Conciliacion demografica y
  proyecciones de poblacion.

Intermediate/summary CSVs are written to `data/` and `data/revision/` and are
small enough to version.

## Requirements

R packages: `httr`, `jsonlite`, `dplyr`, `ggplot2`, `readr`, `duckdb`,
`DBI`, `broom`, `forcats`, `tidyr`, `readxl`, plus the packages loaded at the
top of `analisis_revision_LKE.R`.
