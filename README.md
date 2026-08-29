# Mortality Trend Models: Cardiovascular Disease and Cancer in Mexico (1998-2024)

R code for the regression analysis submitted to LKE 2026 (BUAP).

## Contents

- `Esperanza_de_Vida.Rmd` — full analysis pipeline:
  1. WHO Global Health Observatory data download (NCDMORT3070)
  2. INEGI death-registry aggregation (DuckDB)
  3. CONAPO population data and rate computation
  4. Linear regression (rate ~ year + pandemic indicator)
  5. Pre-pandemic vs. pandemic/post-pandemic models
  6. Quasibinomial logistic regression (cause of death ~ period + sex + age group)
  7. 2030 projection

## Data

Raw source files are not included in this repository due to size
(the INEGI microdata file is ~7 GB). To reproduce the analysis, place
the following files in `data/raw/`:

- `base_defunciones_inegi_1990_2024.csv` — INEGI, Estadísticas de
  Defunciones Registradas (EDR), obtained via INSP.
- `0_Pob_Mitad_1950_2070.xlsx` — CONAPO, Conciliación demográfica y
  proyecciones de población.

All intermediate/summary CSVs produced by the script are written to
`data/` and are small enough to version if desired.

## Requirements

R packages: `httr`, `jsonlite`, `dplyr`, `ggplot2`, `readr`, `duckdb`,
`DBI`, `broom`, `forcats`, `tidyr`, `readxl`.
