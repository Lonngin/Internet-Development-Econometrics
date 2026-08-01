

# Replication Package
## Internet Access and Economic Development: Evidence from Global Panel Data

**Authors**: Georgios Chainis, Nikolaos Koptsis, Lev Ryzvaniuk, Vyronas Trikkalidis  
**Course**: ECO 1S002 — Topics in Economics  
**Institution**: École Polytechnique — Institut Polytechnique de Paris  
**Date**: May 2026

---

# Data Source

The data used in this project comes from the **World Bank World Development Indicators (WDI)** database, a publicly available dataset maintained by the World Bank Group.

- Main Database: https://databank.worldbank.org/source/world-development-indicators
- Metadata Glossary: https://databank.worldbank.org/metadataglossary/world-development-indicators
- Access date: May 2026
- Coverage: Approximately 150 countries, 2005–2024

## Variables

| Variable | Description | WDI Indicator Code |
|---|---|---|
| `gdp_pc` | GDP per capita, PPP (constant international dollars) | `NY.GDP.PCAP.PP.KD` |
| `log_gdp_pc` | Natural logarithm of GDP per capita | Constructed variable |
| `internet` | Individuals using the internet (% of population) | `IT.NET.USER.ZS` |
| `telephone` | Fixed telephone subscriptions (per 100 people) | `IT.MLT.MAIN.P2` |
| `education` | School enrollment, secondary (% gross) | `SE.SEC.ENRR` |
| `urban` | Urban population (% of total population) | `SP.URB.TOTL.IN.ZS` |
| `investment` | Gross capital formation (% of GDP) | `NE.GDI.TOTL.ZS` |
| `telephone_lag` | Lagged fixed telephone subscriptions | Constructed variable |

---

# Project Structure

```text
research_project/
├── input/
│   ├── world_bank_raw.csv
│   └── iv_world_bank_raw.csv
├── output/
│   ├── world_bank_clean.csv
│   ├── iv_world_bank_clean.csv
│   ├── figures/
│   │   └── internet_gdp_plot.png
│   └── tables/
│       ├── summary_statistics.tex
│       ├── regression_table.tex
│       └── iv_regression_table.tex
├── code/
│   ├── 01_data.r
│   ├── 02_analysis.r
│   └── 03_iv_exploration.r
├── report.tex
├── references.bib
└── README.md
```

---

# Replication Instructions

## Requirements

All analysis is conducted in **R**.

Install the required packages:

```r
install.packages(c(
  "WDI",
  "tidyverse",
  "fixest",
  "modelsummary"
))
```

---

# Steps to Replicate

Run the scripts in the following order.

## 1. `01_data.r`

This script:
- downloads raw World Bank data,
- constructs the panel dataset,
- creates derived variables,
- and saves clean datasets.

Outputs:
- `input/world_bank_raw.csv`
- `output/world_bank_clean.csv`

---

## 2. `02_analysis.r`

This script:
- loads the cleaned dataset,
- produces descriptive statistics,
- generates figures,
- estimates OLS and fixed-effects regressions,
- and exports LaTeX regression tables.

Outputs:
- `output/figures/internet_gdp_plot.png`
- `output/tables/summary_statistics.tex`
- `output/tables/regression_table.tex`

The main specifications include:
- pooled OLS,
- OLS with controls,
- country fixed effects,
- country and year fixed effects,
- clustered standard errors at the country level.

---

## 3. `03_iv_exploration.r`

This script:
- constructs an exploratory instrumental-variable specification,
- instruments internet access using lagged fixed telephone subscriptions,
- estimates a two-stage least squares model,
- and exports the IV regression table.

Outputs:
- `output/iv_world_bank_clean.csv`
- `output/tables/iv_regression_table.tex`

The IV specification should be interpreted cautiously because the exclusion restriction may not fully hold.

---

# Econometric Overview

The project estimates the relationship between internet access and economic development using panel-data methods.

## Baseline Specification

The baseline regression estimates:

$$
\log(GDPpc_{it}) = \alpha + \beta Internet_{it} + \varepsilon_{it}
$$

where:
- $GDPpc_{it}$ is GDP per capita,
- $Internet_{it}$ is internet penetration,
- $i$ indexes countries,
- $t$ indexes years.

Additional specifications progressively include:
- controls,
- country fixed effects,
- year fixed effects,
- clustered standard errors,
- and an exploratory IV strategy.

---

# Main Findings

The results show:
- a strong positive raw correlation between internet access and GDP per capita,
- substantially smaller coefficients after introducing controls and fixed effects,
- and a positive but cautious IV estimate.

The project concludes that internet access is strongly associated with economic development, although identifying a fully causal effect remains difficult.

---

# Notes

- All regression tables are exported automatically in LaTeX format.
- Standard errors are clustered at the country level.
- The IV specification is exploratory and should not be interpreted as definitive causal evidence.
- Running all scripts sequentially reproduces the full empirical workflow used in the paper.
