# v2 — Corrected Pipeline

The original notebook rebuilt as one clean pipeline, with the fixes from `../AUDIT.md` applied one at a time. Each fix is marked in the code with a `v2 FIX #` comment.

**Results are provisional** until all open audit items are fixed.

| Fix | Issue | Before | After |
|---|---|---|---|
| #1 | Newey-West SEs multiplied by n | Long-only market beta t = 1.80, alpha t = 0.07 | Market beta t = 31.64, alpha t = 1.31 |
