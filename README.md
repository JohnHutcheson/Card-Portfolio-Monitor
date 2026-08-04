# Card Portfolio Monitor
 
A portfolio-level credit review of a consumer credit card book, built the way a bank credit risk team runs a
monthly monitoring cycle — delinquency profile, roll-rate transitions, vintage performance, expected loss
(PD × LGD × EAD), and an industry benchmark against Federal Reserve data. Each section pairs the analysis with a
plain-English read of what it means for the book, ending in a one-page summary written for leadership.
 
**John C. Hutcheson** · Minneapolis, MN · CFA Level I candidate (February 2027)
 
---
 
## Contents
 
| Section | Analysis | The question it answers |
|---|---|---|
| 1–2 | Portfolio composition, FICO and utilization profile | Who are we lending to? |
| 3 | Delinquency profile, balance- vs account-weighted | Where does the book stand today? |
| 4 | Roll-rate transition matrix | Where do losses come from next quarter? |
| 5 | Vintage / seasoning curves | Is underwriting drifting? |
| 6 | Expected loss by FICO segment | What should we reserve? |
| 7 | FRED industry benchmark | How do we compare — and why? |
| 8 | Leadership one-pager | What does the CFO need in 60 seconds? |
 
## Selected findings
 
- Delinquency runs **3.70% balance-weighted versus 2.14% by account count** — delinquent accounts average
  $7,613 in balance against $4,067 for the rest of the book, so account-based reporting understates the dollars
  at risk by nearly half.
- Expected loss of **$3.9M (4.76% of receivables)** concentrates in the 660–719 segment: 33.8% of balances but
  44.5% of loss — the largest segment, not the riskiest one.
- Exposure at default is **$156.7M against $82.7M of current balances**, because stressed borrowers draw on
  available credit before defaulting. Undrawn lines are exposure; line increases are credit decisions.
- The book's delinquency sits **78bp above the industry benchmark** despite being 91% prime — an inconsistency
  flagged for reconciliation rather than reported as a result.
## Running it
 
1. Open `Card_Portfolio_Monitor.ipynb` in [Google Colab](https://colab.research.google.com) (File → Upload
   notebook) or any local Jupyter install.
2. Run all cells top to bottom. Everything executes out of the box on a seeded synthetic portfolio.
3. Optional: add a free [FRED API key](https://fred.stlouisfed.org) in Section 7 for live industry data;
   published Q1 2026 values are used as a fallback.
`Card_Portfolio_Monitor_Report.pdf` contains the written review in memo form.
 
## Methodology, assumptions & limitations
 
- **Data.** Synthetic portfolio of 20,000 accounts, seeded for reproducibility. FICO, limits, utilization, and
  delinquency are generated with realistic interdependencies; account age is assigned independently, which is why
  no seasoning effect appears in Section 5. Random draws may vary slightly across Python environments.
- **Delinquency.** Balance-weighted (industry convention) across 30/60/90+ DPD buckets, with account-weighted
  figures reported alongside for contrast.
- **Expected loss.** EL = PD × LGD × EAD by FICO segment. PD assumptions are illustrative and directionally
  consistent with published card performance; LGD is 85%, reflecting thin unsecured recoveries; EAD applies a
  40% credit conversion factor to undrawn lines.
- **Roll rates.** Transition probabilities are specified rather than estimated — a single-period snapshot cannot
  support empirical estimation. On real data these derive from month-over-month account-level movements.
- **Benchmark.** Federal Reserve series for credit card delinquency and charge-off rates at all commercial banks
  (FRED: `DRCCLACBS`, `CORCCACBS`), Q1 2026.
- **Before use on real balances.** Inputs would require validation against internal loss experience, definitional
  alignment between internal delinquency flags and the benchmark series, empirical estimation of roll rates and
  credit conversion factors, and documented governance review consistent with model risk management expectations.
## Tools
 
Python · pandas · NumPy · matplotlib · Jupyter · FRED API
