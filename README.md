# SESI  
## Spain Energy Stress Index  
### A Regime-Aware Stress Benchmark for the Spanish Power Market  

---

## Overview

SESI, the Spain Energy Stress Index, is a percentile-based regime benchmark designed to measure and contextualize stress conditions in the Spanish day-ahead electricity market.

The framework decomposes market conditions into three complementary layers: realized stress, structural regime distance, and forward expectations.

SESI is not a trading signal.  
It is not a probability model.  
It is a reproducible stress classification framework.

The objective is to provide a structured way to interpret power market regimes using transparent methodology and publicly available data.

---

## What SESI Does

SESI converts complex market behavior into a normalized 0 to 100 percentile scale.

A higher percentile indicates that current conditions are more extreme relative to historical observations.

The index separates:

Realized cyclical stress based on short-term price dislocation and volatility.

Structural regime distance measured relative to the 2018 to 2020 baseline.

Forward expectations alignment using OMIP futures percentiles.

This decomposition allows regime identification without relying on discretionary narrative.

---

## Data Sources

SESI is built exclusively on publicly accessible data.

Spot market data  
OMIE day-ahead marginal prices, daily frequency, from 2018 to present.

Gas proxy  
TTF continuous futures, used to measure structural gas regime distance relative to the 2018 to 2020 reference period.

Futures overlay  
OMIP month base contracts, aggregated as 1 to 3 month average and converted into percentile rankings versus the pre-2022 distribution.

No proprietary data feeds are required.

---

## Model Specification

The core model is frozen and versioned.

Features include short-term price z-score versus trailing 30-day distribution, structural price z-score versus 2018 to 2020 baseline, normalized 7-day volatility, and structural gas z-score.

The model is trained using ridge regression on the period 2018-01-01 to 2021-12-31.

The training target is the maximum absolute price move over the following seven days.

The full 2022 crisis period is excluded from training and used strictly for out-of-sample validation.

The raw model output is transformed into percentile rankings.

SESI is defined as the expanding percentile of the raw score relative to historical observations up to time t.

SESI_structural is defined as the percentile of the raw score relative only to the fixed pre-2022 reference distribution.

There is no look-ahead bias in feature construction, model training, or percentile computation.

---

## Interpretation Framework

SESI values range from 0 to 100.

A value of 80 means that current stress is higher than 80 percent of historical observations.

It does not imply an 80 percent probability of crisis.  
It does not imply expected return direction.

Structural and realized layers are interpreted jointly.

When both SESI and SESI_structural are elevated, the system is in a structurally tight regime.

When SESI is high but structural is moderate, the regime reflects short-term shock dynamics.

Forward dislocation is defined as the difference between OMIP forward percentile and SESI_structural percentile.

Large negative values indicate forward discounting relative to structural stress.

Large positive values indicate forward risk premium above structural stress.

---

## Validation

SESI has been evaluated on the 2021 to 2022 energy crisis as a strictly out-of-sample case study.

The index entered extreme percentile regimes during late 2021 and remained elevated throughout 2022.

Structural percentiles reached the upper historical boundary during the crisis plateau.

Forward percentiles remained broadly aligned with structural stress during peak periods.

Validation is descriptive and conditional.  
It does not establish causality and does not claim forecasting power.

---

## Use Cases

SESI is designed for regime awareness and structured stress monitoring.

Potential applications include risk monitoring, energy procurement planning, macro regime communication, stress event identification, and forward dislocation analysis.

The framework is suitable for integration into analytics platforms, risk dashboards, and macro research workflows.

---

## Versioning

The SESI core specification is frozen and version-controlled.

Changes to methodology, reference windows, or feature construction are documented and versioned explicitly.

Reproducibility is a primary design principle.

---

## Monetization and Integration

SESI is designed to be API-ready.

Structured endpoints can provide current regime state, historical stress series, threshold events, and quadrant classification.

The framework is suitable for integration into broader energy analytics ecosystems as a regime benchmark layer.

---

## Contact

For research collaboration, integration discussions, or API access inquiries:

hello@getparagua.com

SESI is developed as a long-term regime taxonomy framework for Iberian power markets.
