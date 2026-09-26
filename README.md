# Small-Cap Quality Factor Portfolio

> **Status: v2 rebuild in progress.** An audit of the original course pipeline found errors that affect the reported results (see [AUDIT.md](AUDIT.md)). Results will be published here only after the corrected pipeline is rerun.

## Question

Does screening small-cap U.S. stocks on accounting-based **quality** improve on a naive small-cap index (IWM)? The approach follows the quality framework of Asness, Frazzini & Pedersen.

## Method

- **Universe:** U.S. common stocks (NYSE/AMEX/NASDAQ) between the 20th and 50th NYSE market-equity percentiles, price ≥ $5 at each rebalance
- **Quality score:** equal-weighted average of cross-sectional z-scores of five measures:
  - Safety: earnings volatility (lower is better)
  - Payout: net payout yield
  - Investment: CAPX / total assets (lower is better)
  - Profitability: return on assets
  - Growth: five-year change in net income scaled by assets
- **Look-ahead control:** fiscal-year accounting data is used only from June of the following calendar year
- **Portfolio:** top 200 stocks by quality score, equal-weighted, rebalanced quarterly
- **Tests:** quintile sorts, Fama-French 3-factor regressions (long-short and long-only), benchmark statistics, stress periods (GFC, Covid crash, 2022 rate shock)

## Repository structure

- `original/` — course notebook as submitted (kept unchanged for reference)
- `v2/` — corrected pipeline (in progress)
- `AUDIT.md` — issues found in the original pipeline and how each is fixed

## Data

Data comes from CRSP and Compustat via WRDS and the Ken French Data Library. **WRDS data is licensed, so it is not included in this repo.** To run the code you need your own WRDS access; the expected input files are listed at the top of the notebook.

## Credits

This project began as a four-person team assignment for FINA 6334 (Empirical Methods in Finance, Northeastern, Spring 2026) with Aryaa Shah, Yuvraj Chawla and Sanskar Jain. The pipeline audit, bug fixes and v2 rebuild in this repo are my independent work.

## Roadmap

- [ ] Publish original notebook and audit findings
- [ ] Fix Newey-West standard errors
- [ ] Remove duplicate benchmark months
- [ ] Hold positions through the full quarter
- [ ] Use Ken French NYSE breakpoints
- [ ] Link CRSP–Compustat via CCM `LPERMNO` with link dates
- [ ] Rerun and publish corrected results
- [ ] Extension: machine-learning weighting of quality signals
