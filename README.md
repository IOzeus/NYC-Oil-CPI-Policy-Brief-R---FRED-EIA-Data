# NYC Oil CPI Policy Brief R - FRED/EIA Data

A university econometrics project framed as a confidential policy brief to the NYC Mayor's Office of Management and Budget (OMB), analysing the passthrough effects of the 2026 Iran conflict oil shock on fuel prices and consumer inflation in New York City.

## Background

In early 2026, WTI crude oil surged from ~$64/barrel in February to a peak of ~$102/barrel in May — a 59% increase over three months driven by the Iran conflict. This project models how that shock transmitted through retail fuel prices to broader consumer inflation (CPI) in the NYC metro area.

## Data

- **Source:** FRED (Federal Reserve Bank of St. Louis) and EIA (U.S. Energy Information Administration)
- **Coverage:** June 2000 – August 2026 (~315 monthly observations)
- **Series:**
  - WTI Crude Oil Price ($/barrel)
  - Midgrade Gasoline — NY/NJ Metro ($/gallon)
  - Premium Gasoline — NY/NJ Metro ($/gallon)
  - Diesel — Mid-Atlantic Region ($/gallon)
  - NY-NJ-PA CPI (All Urban Consumers)

## Methods

- **Stationarity Testing:** ADF and KPSS tests — all five series confirmed I(1)
- **Cointegration:** Phillips-Ouliaris and Johansen Trace/Max-Eigenvalue tests
- **Passthrough Analysis:** ARDL models (levels for oil-to-fuel; log-differenced for fuel-to-CPI and oil-to-CPI)
- **VECM:** Rank 2, K=6 lags, seasonal dummies — jointly models oil, midgrade, and CPI
- **Impulse Response Functions:** Cholesky decomposition (ordering: oil → midgrade → CPI)
- **Forecast Error Variance Decomposition (FEVD)**

## Key Findings

**Full Passthrough Summary:**

| Relationship | Model | Short-Run | Long-Run | R² |
|---|---|---|---|---|
| Oil → Midgrade | ARDL (levels) | $0.015 / $1 | $0.033 / $1 | 98.3% |
| Oil → Premium | ARDL (levels) | $0.015 / $1 | $0.036 / $1 | 98.5% |
| Oil → Diesel | ARDL (levels) | $0.018 / $1 | $0.049 / $1 | 98.7% |
| Midgrade → CPI | ARDL (log-diff) | 0.039% / 1% | 0.042% / 1% | 36.5% |
| Premium → CPI | ARDL (log-diff) | 0.041% / 1% | 0.044% / 1% | 36.8% |
| Diesel → CPI | ARDL (log-diff) | 0.039% / 1% | 0.045% / 1% | 29.2% |
| Oil → CPI | ARDL (log-diff) | 0.014% / 1% | 0.023% / 1% | 27.0% |

**2026 Iran Conflict Validation:**
- 59% oil price increase → model-predicted +1.4% CPI
- Actual CPI change over same period: +2.3% (model captures a meaningful share; remainder attributable to broader supply chain disruption)

**VECM / IRF / FEVD:**
- Oil weakly exogenous to the long-run relationships (midgrade adjusts, oil does not)
- Oil shock lifts midgrade ~5% at peak (months 1–3), remaining elevated over 24-month horizon
- Oil accounts for ~43% of CPI forecast error variance from month 6 onward
- Diesel identified as the key leading indicator for NYC freight and transit cost pressures given its highest long-run passthrough

## Limitations

- Structural breaks at 2008 (GFC), 2020 (COVID), and 2026 (Iran conflict) not explicitly modelled
- Nominal prices used throughout — no deflation
- Some residual serial dependence in VECM at 12-lag horizon
- Oil weakly exogenous assumption holds statistically but not guaranteed under policy interventions

## Tools

R — `urca`, `vars`, `tseries`, `ggplot2`, `dplyr`
