# SESI  
## Spain Energy Stress Index  
### A Regime-Aware Stress Benchmark for the Spanish Power Market  

---

## Overview

SESI, the Spain Energy Stress Index, is a percentile-based regime benchmark designed to measure and contextualize stress conditions in the Spanish day-ahead electricity market.

The framework decomposes market conditions into three complementary layers:

- Realized stress  
- Structural regime distance  
- Forward expectations alignment  

SESI is not a trading signal.  
SESI is not a probability model.  
SESI is a reproducible stress classification framework.

Its objective is to provide a structured, transparent way to interpret power market regimes using publicly available data.

---

## What SESI Does

SESI converts complex market behavior into a normalized 0 to 100 percentile scale.

A higher percentile indicates that current conditions are more extreme relative to historical observations.

The index separates:

- Realized cyclical stress based on short-term price dislocation and volatility  
- Structural regime distance measured relative to the 2018 to 2020 baseline  
- Forward expectations alignment using OMIP futures percentiles  

This decomposition enables regime identification without discretionary narrative.

---

## Data Sources

SESI is built exclusively on publicly accessible data.

**Spot market data**
- OMIE day-ahead marginal prices  
- Daily frequency  
- 2018 to present  

**Gas proxy**
- TTF continuous futures  
- Structural z-score relative to 2018 to 2020 baseline  

**Futures overlay**
- OMIP month base contracts  
- 1 to 3 month average settlement  
- Percentile versus pre-2022 distribution  

No proprietary data feeds are required.

---

## Model Specification

The core model is frozen and versioned.

**Feature set**

- Short-term price z-score versus trailing 30-day distribution  
- Structural price z-score versus 2018 to 2020 baseline  
- Normalized 7-day volatility  
- Structural gas z-score  

**Training design**

- Ridge regression  
- Training window: 2018-01-01 to 2021-12-31  
- Target: maximum absolute price move over the following 7 days  
- 2022 fully excluded from training  

**Score construction**

- Raw model output transformed into percentile rankings  
- SESI defined as expanding percentile of raw score up to time t  
- SESI_structural defined as percentile relative to fixed pre-2022 reference distribution  
- No look-ahead bias  

---

## Interpretation Framework

SESI values range from 0 to 100.

- A value of 80 means stress is higher than 80 percent of historical observations  
- It does not imply probability of crisis  
- It does not imply price direction  

Joint interpretation:

- High SESI and high SESI_structural indicate structurally tight regime  
- High SESI with moderate structural suggests short-term shock  
- Forward dislocation defined as OMIP percentile minus SESI_structural  

Dislocation interpretation:

- D ≤ -25 indicates forward discounting  
- D ≥ +25 indicates forward risk premium  

---

## Validation

SESI has been evaluated on the 2021 to 2022 energy crisis as a strictly out-of-sample case study.

Key observations:

- Extreme percentile entry during late 2021  
- Sustained structural elevation throughout 2022  
- Forward percentiles broadly aligned with structural stress  
- Plateau behavior rather than isolated spikes  

Validation is descriptive and conditional.  
No forecasting claim is made.

---

## Use Cases

SESI supports:

- Risk monitoring  
- Regime communication  
- Energy procurement planning  
- Stress awareness  
- Forward dislocation analysis  
- Integration into analytics platforms  

It is designed as a regime benchmark layer within broader energy analytics systems.

---

## Versioning

- Core specification frozen  
- Explicit version control  
- Documented methodological changes  
- Reproducibility prioritized  

---

## Monetization and Integration

SESI is API-ready.

Potential structured endpoints include:

- Current regime state  
- Historical stress series  
- Threshold crossing events  
- Quadrant classification  

Designed for integration into energy analytics platforms, risk systems, and macro dashboards.

---

## Contact

For research collaboration, integration discussions, or API access inquiries:

hello@getparagua.com

SESI is developed as a long-term regime taxonomy framework for Iberian power markets.
