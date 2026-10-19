# Mortality Trend Models: Cardiovascular Disease and Cancer in Mexico (1998–2024)

R code for the analysis submitted to LKE 2026 (BUAP), revised version for POLIBITS.

## Contents

- `Esperanza_de_Vida.Rmd` — original pipeline:
  1. WHO Global Health Observatory data download (NCDMORT3070)
  2. INEGI death-registry aggregation (DuckDB)
  3. CONAPO population data and rate computation
  4. Linear regression (rate ~ year + pandemic indicator)
  5. Pre-pandemic vs. pandemic/post-pandemic models
  6. Quasibinomial logistic regression (cause of death ~ period + sex + age group)
  7. 2030 projection
- `analisis_revision_LKE.R` — revision analyses (run after the .Rmd, which
  produces the base tables in `data/`; writes outputs to `data/revision/`):
  ICD-10 definitions and year assignment checks, crude / age-specific /
  age-standardized rates (WHO standard population), Kitagawa decomposition,
  serial-dependence diagnostics, alternative trend specifications (HAC, AR(1),
  quadratic), pandemic-window sensitivity, interrupted time series,
  counterfactual, rolling-origin out-of-sample evaluation, logistic model
  sensitivity checks, and WHO comparison on compatible ages (30–69).
- `proyeccion_2030_escenarios.R` — 2030 scenarios (A, B, C) using CONAPO's age
  structure plus linear-model prediction intervals. Run in the same R session
  right after `analisis_revision_LKE.R`.
- `nlp/` (optional, see below) — YouTube comment collection, cleaning and
  sentiment analysis (Python).

## Data

Raw source files are not included in this repository due to size
(the INEGI microdata file is ~7 GB). To reproduce the analysis, place
the following files in `data/raw/`:

- `base_defunciones_inegi_1990_2024.csv` — INEGI, Estadísticas de
  Defunciones Registradas (EDR), obtained via INSP.
- `0_Pob_Mitad_1950_2070.xlsx` — CONAPO, Conciliación demográfica y
  proyecciones de población.

All intermediate/summary CSVs produced by the scripts are written to
`data/` and `data/revision/` (files `01_…` to `22_…`) and are small enough
to version.

## Sentiment analysis (Section VI of the paper)

- Comments: collected with the YouTube Data API v3 (7 search phrases, up to
  10 videos each, up to 50 comments per video). The API key is **not** included;
  set it as an environment variable and never commit it.
- Model: `pysentimiento` (RoBERTuito), task `sentiment`, language `es`.
- Evaluation: 100 randomly sampled comments labeled independently by two
  annotators; metrics are accuracy, macro-F1 and Cohen's κ with bootstrap
  intervals. Only the comment text, not the model output, was shown to annotators.
- Include in `nlp/`: the notebook (with the API key removed), the cleaned
  comments CSV, the labeling sheet, and `evaluar_etiquetado.py`. Leave out the
  model-output key file if you do not want to publish individual predictions.

## Requirements

R (≥ 4.2) packages: `httr`, `jsonlite`, `dplyr`, `ggplot2`, `readr`, `duckdb`,
`DBI`, `broom`, `forcats`, `tidyr`, `readxl`, plus the packages loaded at the top
of `analisis_revision_LKE.R` (check its header; typically `sandwich`, `lmtest`,
`nlme`).

Python (sentiment analysis): `pandas`, `numpy`, `openpyxl`, `pysentimiento`,
`google-api-python-client`, `emoji`, `nltk`.
