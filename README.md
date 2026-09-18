# Data Quality Profiling — Big Mac Index

## Objective
This project audits a well-known cross-country panel dataset — The Economist's Big Mac Index — for common data quality pitfalls, quantifying how naive handling of missing observations and a swapped-ratio computation error can silently bias economic conclusions.

## Methodology
- Diagnosed and corrected a purchasing power parity (PPP) computation error caused by a swapped numerator/denominator in the valuation formula, which had inverted the ranking of overvalued and undervalued currencies.
- Identified a survivorship bias introduced by dropping all countries with incomplete time coverage before computing summary statistics, rather than working with the full unbalanced panel.
- Quantified that bias empirically by comparing the average Big Mac price across "complete-panel" countries only against the average across all countries available in each period.
- Built a reusable `profile_dataframe()` function to classify any tabular dataset (cross-sectional, time series, or panel), assess panel balance, and report per-column missingness.

## Key Findings
- The corrected PPP calculation places Switzerland, Uruguay, and Norway as the most overvalued currencies and Taiwan, Indonesia, and Egypt as the most undervalued — reversing the incorrect ranking produced by the original bug.
- Filtering to countries with complete 45-period panels drops 32 of 57 countries and overstates the global average Big Mac price by approximately $0.081 (2.1%), with the complete-panel average running higher in 33 of 45 periods — demonstrating that convenience-sample filtering introduces a measurable, directional bias rather than random noise.
- Profiling the full panel confirms 57 countries across 45 time periods, with only 25 countries observed in every period, making the dataset an unbalanced panel by construction.
