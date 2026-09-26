# Audit of the Original Pipeline

I reviewed the original course notebook line by line and checked its outputs against the submitted report. This file records what I found and how each issue is being fixed.

## Summary

The saved notebook outputs do not match the numbers in the submitted report (e.g. long-short alpha 0.090%/mo, t = 0.51 in the notebook vs 0.199%/mo, t = 1.34 in the report). The report's results cannot be reproduced from this code, so **v2 results will be rebuilt from scratch and only verified numbers will be reported.**

## Issues

| # | Issue | Effect | Fix | Status |
|---|---|---|---|---|
| 1 | Newey-West function multiplies the covariance matrix by *n* | Every long-only t-stat shrunk by √310 ≈ 17.6× (e.g. market beta t = 1.8 instead of ~32) | Remove the factor of *n*; verified against plain OLS on simulated data | Open |
| 2 | IWM file contains duplicate months (314 rows for 308 months) | Six months counted twice in cumulative returns, drawdowns and regressions | Drop duplicates before merging | Open |
| 3 | Holdings leave the portfolio mid-quarter if they exit the size band, fall below $5, or have a missing return | Portfolio averages 189 stocks, not 200; returns are biased | Hold selected stocks until the next rebalance | Open |
| 4 | NYSE breakpoints computed from our own data after the $5 filter | Cutoffs biased upward vs the specified definition | Use Ken French's ME breakpoints file | Open |
| 5 | CRSP–Compustat link via header CUSIP with no link dates | Missed matches (~57% coverage) and possible duplicate stock-months | Link on CCM `LPERMNO` with `LINKDT`/`LINKENDDT` and primary-link filters | Open |
| 6 | Report states 1st/99th winsorization; not found in the notebook | Outliers may distort z-scores | Verify upstream file; add winsorization explicitly | Open |
| 7 | Quintiles re-sorted monthly; spec requires sorting at quarterly rebalances | Inconsistent with portfolio construction | Sort at rebalance dates only | Open |
| 8 | Long-short uses OLS SEs; long-only uses Newey-West | Inconsistent inference | Use Newey-West for both | Open |
| 9 | Documents say 2000–2024; data runs to Dec 2025 | Mismatched sample description | Fix sample dates explicitly | Open |

## Items to verify

- Whether CRSP CIZ `MthRet` already incorporates delisting returns
- Whether a US-incorporation filter is needed to match share codes 10/11
- Whether the long-short regression should subtract the risk-free rate (Q5 − Q1 is already a zero-cost return)
