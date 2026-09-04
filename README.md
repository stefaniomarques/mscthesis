# The Price Elasticity of Residential Gas Demand in Ireland

**Evidence Across the COVID-19 Pandemic and the 2022 Energy Crisis**

MSc Economics and Data Analytics Thesis · University College Dublin · 2026
Author: Stefanio Marques · Supervisor: Dr. Ciara Whelan

---

## Overview

This project estimates how sensitive Irish households are to changes in natural gas
prices, and tests whether two major shocks — the 2020 COVID-19 pandemic and the 2022
European energy crisis — changed that sensitivity. The question matters directly for
climate policy: Ireland's Climate Action Plan leans heavily on carbon taxation to push
households toward electric heat pumps, and that strategy only works if demand actually
responds to price.

Using 44 quarterly observations (2014 Q1–2024 Q4), the analysis combines CSO metered
gas volumes, energy price indices, real household consumption, building energy rating
data, and heating degree days into a single econometric framework.

## Key Findings

| Result | Value |
|---|---|
| Static price elasticity of demand | **−0.334** (p = 0.006) |
| ARDL long-run price elasticity | **−0.367** (p = 0.012) |
| ARDL bounds test F-statistic (cointegration) | **48.487** (upper bound 3.79 → reject H₀) |
| Error-correction speed | **87.9%** of disequilibrium corrected per quarter |
| Structural break (pandemic / energy crisis) | Not statistically detectable at this sample size |

**Headline takeaway:** residential gas demand in Ireland is price-inelastic and stays
inelastic even across two major economic shocks. Price signals alone — including
carbon taxes — are unlikely to drive fast fuel-switching without complementary capital
investment in retrofits and heat pumps.

## Methodology

- **Framework:** ARDL bounds-testing approach ([Pesaran, Shin & Smith, 2001](https://doi.org/10.1002/jae.616)), chosen because
  the regressors are a mix of I(0) and I(1) series, which rules out Engle-Granger or
  Johansen cointegration methods.
- **Specification:** ARDL(1,0,0,1,0,1), selected by AIC, estimated via an
  error-correction model to separate short-run dynamics from the long-run equilibrium.
- **Identification challenge:** gas and electricity prices are highly collinear
  (r = 0.990). Resolved with an identified relative-price reparameterisation
  (`ln(P_gas) − ln(P_elec)`) — an exact algebraic transform of the separate-price-levels
  model, isolating the response to a common energy-price movement.
- **Structural break testing:** Chow-type joint tests on pre-specified shock windows,
  plus an endogenous Gregory-Hansen (1996) break search as a robustness check.
- **Diagnostics:** ADF/KPSS unit root tests, VIF collinearity checks, Breusch-Pagan,
  Durbin-Watson, Jarque-Bera, and a CUSUM parameter-stability test.
- **Statistical power:** every null structural-break result is reported alongside its
  minimum detectable effect size, rather than treated as proof of no effect.

## Tech Stack

- **R** — `ARDL`, `aod`, `cointReg`, `csodata`, `flextable`
- **Quarto** (`.qmd`) — reproducible document combining analysis and write-up
- **LaTeX / LuaLaTeX** — thesis typesetting
- **Python** (`pandas`, `statsmodels`) — independent cross-check of summary statistics,
  ADF results, and OLS coefficients

## Repository Structure

```
mscthesis/
├── README.md
├── analysis/          # R / Quarto estimation scripts
├── data/               # Data sources and construction notes (raw data not included — see below)
├── output/
│   ├── figures/         # Key charts (elasticity plot, cointegration tracking)
│   └── tables/           # Full-precision regression output
└── docs/                 # Thesis abstract / summary write-up
```

## Data Availability

The underlying series are compiled from public CSO (Central Statistics Office Ireland)
and Met Éireann sources. Raw data is not redistributed here; `data/README.md` lists
each source table and how to retrieve it directly.

## Reproducing the Analysis

```r
# Install dependencies
install.packages(c("ARDL", "aod", "flextable", "csodata"))

# Run the estimation
quarto::quarto_render("analysis/thesis_main.qmd")
```

## Notes

This repository presents a summary of an academic thesis submitted in partial
fulfilment of the MSc Economics and Data Analytics at University College Dublin. Full
analysis code is being progressively added — see `analysis/` for current contents.
