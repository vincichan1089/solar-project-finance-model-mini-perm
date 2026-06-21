# APAC Project Finance Model — Utility-Scale Solar PV

> **Built from scratch in 8 hours** as a take-home modeling test for a European bank's APAC project finance team.

This Excel-based project finance model covers a **200 MWdc / 160 MWac utility-scale solar PV project** in the Australian NEM, featuring a hybrid PPA + merchant revenue structure, DSCR-based debt sizing, mini-perm financing, and a full three-statement financial model.

---

## Project Overview

| Parameter | Assumption |
|---|---|
| Installed capacity | 200 MWdc / 160 MWac |
| Net capacity factor (P50) | 24.0% |
| Degradation | 0.5% p.a. (compounding from Year 2) |
| Marginal Loss Factor (MLF) | 0.88 (static) |
| EPC / Total project cost | AUD 220,000,000 |
| Financial close | 31 Dec 2026 |
| Commercial Operation Date | 1 Jan 2028 |
| Project life | 35 years (decommission: 31 Dec 2062) |
| Corporate tax rate | 30% (straight-line depreciation, 20-year useful life) |

---

## Revenue Structure

The project sells electricity under a **dual-tranche revenue structure**:

- **Contracted (PPA):** 65% of net generation sold at AUD 75/MWh (flat, no escalation) for 10 years from COD
- **Merchant:** 35% of net generation sold at spot, with 2028 spot price of AUD 55/MWh escalating at 2.0% p.a.; a 5% negative pricing coefficient is applied to reflect curtailment/negative price hours
- **Merchant Intensity:** 54.1% — calculated as the PV of merchant CFADS divided by total PV of CFADS over the notional debt life, reflecting meaningful but manageable uncontracted revenue exposure

Upon PPA expiry (Year 11), 100% of revenue becomes merchant, escalating through the remaining 25-year tail.

---

## Debt Sizing & Structure

Debt is sized by **iterating to a minimum DSCR floor of 1.35x** over the notional 25-year amortization profile. The mini-perm structure matures after 5 years, with the residual bullet refinanced at maturity.

| Metric | Value |
|---|---|
| Target debt size | AUD 131,825,074 |
| Gearing (% of total project cost incl. IDC) | 57.7% |
| Mini-perm tenor | 5 years |
| Notional amortization profile | 25 years |
| Interest rate (all-in, swapped) | 6.5% p.a. |
| DSRA | 6 months of forward debt service (letter of credit) |
| LC fee | 2.0% p.a. |
| Minimum DSCR (Year 1–5) | 1.35x |
| Average DSCR (Year 1–5) | 1.36x |
| LLCR (notional loan life) | 1.23x |

Debt is **fully repaid via scheduled amortization + cash sweep prepayment** during Years 1–5, with a bullet repayment of the residual balance at mini-perm maturity. The model does **not** model a refinancing at maturity; true equity returns are contingent on refinancing terms.

---

## Returns Summary

| Metric | Value | Note |
|---|---|---|
| Project IRR (P-IRR) | 3.9% | Suppressed by tax shield timing; NOL pool defers tax to Year 21 |
| Debt IRR (D-IRR) | 6.5% | Equal to the all-in swap rate |
| Equity IRR (E-IRR) | 4.1% | Dividends commence Year 14; no refi modelled |
| Breakeven price factor | 0.81 | Goalseeked — PPA at ~AUD 60.7/MWh, spot at ~AUD 44.5/MWh |

**Note on P-IRR vs E-IRR spread:** The levered entity generates a net operating loss (NOL) pool in Years 1–5 due to interest deductions, deferring tax payments to Year 21. On an unlevered basis, tax is payable from Year 1 with no carry-forward, reducing early-year cash flows. The spread between P-IRR and E-IRR reflects the **timing value of the tax shield**, not project underperformance.

---

## Sensitivity Analysis

Six downside scenarios stress-tested against the base case:

| Scenario | Debt Size (AUD) | Min. DSCR | Avg DSCR | LLCR | P-IRR | E-IRR |
|---|---|---|---|---|---|---|
| **Base** | 131,825,074 | 1.35x | 1.36x | 1.23x | 3.9% | 4.1% |
| Spot –15% | 124,059,666 | 1.35x | 1.37x | 1.17x | 2.8% | 2.6% |
| P90 generation | 113,916,347 | 1.35x | 1.37x | 1.24x | 2.9% | 2.8% |
| Curtailment 5% | 129,085,424 | 1.35x | 1.36x | 1.21x | 3.5% | 3.6% |
| OPEX +10% | 127,023,053 | 1.35x | 1.37x | 1.23x | 3.5% | 3.7% |
| MLF 0.82 | 119,590,545 | 1.35x | 1.37x | 1.24x | 3.2% | 3.2% |
| Interest +1% | 120,467,481 | 1.35x | 1.36x | 1.24x | 3.8% | 3.9% |

---

## Model Structure

The workbook is organized across the following sheets:

| Sheet | Contents |
|---|---|
| **Summary** | Key outputs dashboard: debt size, DSCR, LLCR, IRRs, merchant intensity, breakeven pricing |
| **Sensitivity** | Scenario table across 6 downside cases |
| **Input** | All user-controlled assumptions (dates, generation, capex, revenue, opex, financing) |
| **Model** | Core calculation engine: generation, revenue waterfall, CFADS, debt sizing, DSRA, IRRs |
| **FS** | Summarized financial statements (Income Statement, Cash Flow Statement, Balance Sheet) |

---

## Key Modeling Features

- **DSCR-based debt sculpting** — debt sized by goalseeking to a minimum DSCR constraint over a notional repayment profile
- **Mini-perm structure** — scheduled amortization + mandatory cash sweep during the 5-year debt tenor, with bullet repayment at maturity
- **Merchant intensity metric** — ratio of PV of merchant CFADS to total PV of CFADS, used to quantify uncontracted revenue risk
- **NOL / tax loss carry-forward** — corporate tax model with loss utilization logic; tax deferred to Year 21
- **Separate levered vs. unlevered tax** — enables accurate P-IRR calculation and explanation of IRR spread
- **LLCR** — discounted at the debt rate over the notional loan life; used alongside DSCR for debt sizing validation
- **Sources & uses** — IDC funded with equity (CFADS insufficient to support higher debt at 1.35x DSCR floor)
- **Three-statement model** — integrated income statement, cash flow statement, and balance sheet with balance check
- **Full 35-year projection** — annual periods from COD (2028) through decommissioning (2062)

---

## Context

This model was built **from scratch within an 8-hour take-home case study** administered by a European bank's APAC project finance team. No templates or prior models were used as a starting point. The brief provided a project description, key technical assumptions, and a set of output requirements.

The exercise was designed to test the ability to:
- Structure a project finance model architecture independently
- Apply standard debt sizing and credit metric methodology
- Handle nuanced tax and accounting treatment (NOL, depreciation, tax shield)
- Interpret and communicate results clearly under time pressure

---

## About

**Vinci Chan** | BEcon/Finance, The University of Hong Kong  
Project finance & structured finance | APAC energy transition  
[GitHub](https://github.com/vincichan1089) · [LinkedIn](https://www.linkedin.com/in/vincichan1089)
