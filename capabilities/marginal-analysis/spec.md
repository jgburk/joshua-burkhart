---
type: spec
capability: marginal-analysis
engagement: perfect-competition
date: 2026-10-16
status: audited     # draft | built | audited
built_with: openpyxl script by Claude Code from this file; solved with Excel Solver (GRG Nonlinear)
---

# Marginal analysis — model specification

## Purpose

This model decides how many beds to plant for each crop, in order to maximize profits. The model uses constraints and cost functions and solves an optimization problem to find the best answer.

## Inputs — the named contract

| Name | Value | Unit | Source |
|---|---|---|---|
| `weeks` | 36 | weeks per season | Case givens, The farm |
| `fixed_cost` | 20000 | USD per season | Case givens, The farm |
| `beds_max` | 64 | beds, all crops | Case givens, The farm |
| `owner_pay` | 50000 | USD per season | Case givens, The farm |
| `hrs_per_wk` | 40 | paid hours per week | Case givens, The farm |
| `field_share` | 0.50 | share of owner paid hours in the field | Case givens, The farm |
| `owner_paid_hrs` | `= hrs_per_wk × weeks` (1,440) | hours per season | Derived |
| `perm_field_hrs` | `= owner_paid_hrs × field_share` (720) | hours per season | Derived |
| `perm_rate` | `= owner_pay ÷ owner_paid_hrs` (34.72) | USD per hour | Derived |
| `temp_max` | 4 | workers | Case givens, The farm |
| `temp_pay` | 25000 | USD per worker per season | Case givens, The farm |
| `temp_hrs_per_worker` | `= hrs_per_wk × weeks` (1,440) | field hours per worker per season | Derived |
| `temp_rate` | `= temp_pay ÷ temp_hrs_per_worker` (17.36) | USD per hour | Derived |
| `cap_t` / `cap_c` / `cap_m` | 20 / 20 / 30 | beds | Case givens, crop table |
| `price_t` / `price_c` / `price_m` | 8800 / 2094 / 2700 | USD revenue per bed per season | Case givens, crop table |
| `hrs_t` | 2.5 | field hours per week per bed | Case givens, crop table |
| `hrs_c` | `= hrs_t ÷ 3` (0.833) | field hours per week per bed | Case givens, crop table |
| `hrs_m` | `= hrs_t ÷ 2` (1.25) | field hours per week per bed | Case givens, crop table |
| `fert_t` / `fert_c` / `fert_m` | 880 / 440 / 880 | USD per bed per season | Case givens, crop table |
| `dim_t` / `dim_c` / `dim_m` | 0.10 / 0.025 / 0.0125 | share per bed | Case givens, crop table |

## Structure

Two sheets, `Model` and `Schedules`.

- `Model` — INPUTS (farm): the farm givens and derived rates; INPUTS (crops): caps, prices, hours, fertilizer, and diminishing returns per crop; DECISION: the three bed counts Solver changes and `beds_total`; LABOR: hours per crop, owner and temp hours, temp workers, labor cost, blended rate; FARM P&L: revenue, fertilizer, and labor cost per crop; PROFIT: `profit_total`, the Solver objective; CHECKS: each validation rule as a TRUE/FALSE cell, green or red, and `all_checks`; SOLVER MODEL: the saved Solver setup.
- `Schedules` — one standalone VC, MC, and AVC table per crop from q = 0 to its cap, with the crossing cells `cross_t`, `cross_c`, `cross_m`.

## Calculation logic

```
q_tomato, q_carrot, q_mesclun = beds planted (decision cells, whole numbers)

labor_hrs_t = q_tomato  × hrs_t × weeks × (1 + dim_t)^q_tomato
labor_hrs_c = q_carrot  × hrs_c × weeks × (1 + dim_c)^q_carrot
labor_hrs_m = q_mesclun × hrs_m × weeks × (1 + dim_m)^q_mesclun
total_hrs   = labor_hrs_t + labor_hrs_c + labor_hrs_m

perm_used    = MIN(total_hrs, perm_field_hrs)
temp_hrs     = MAX(0, total_hrs − perm_field_hrs)
temp_workers = temp_hrs ÷ temp_hrs_per_worker
labor_cost   = perm_used × perm_rate + temp_hrs × temp_rate
blended_rate = IF(total_hrs = 0, 0, labor_cost ÷ total_hrs)
labor_cost_x = labor_hrs_x × blended_rate          (each crop)

revenue_x    = q_x × price_x                        (each crop)
fert_cost_x  = q_x × fert_x                         (each crop)
profit_total = Σ revenue_x − labor_cost − Σ fert_cost_x − fixed_cost

Marginal-cost schedules, one per crop, q = 0 to cap_x, each crop planted alone:
VC_x(q)  = MIN(H, perm_field_hrs) × perm_rate + MAX(0, H − perm_field_hrs) × temp_rate + q × fert_x,
           where H = q × hrs_x × weeks × (1 + dim_x)^q
MC_x(q)  = VC_x(q) − VC_x(q − 1)
AVC_x(q) = VC_x(q) ÷ q   (blank at q = 0)

Solver: maximize profit_total by changing q_tomato, q_carrot, q_mesclun;
q_x <= cap_x, q_x integer, q_tomato + q_carrot + q_mesclun <= beds_max,
temp_workers <= temp_max; GRG Nonlinear, Integer Optimality 0%.
```

## Conventions

- The $20,000 is a fixed cost.
- The owner's 720 field hours are used before any temporary hours.
- Each crop's labor cost = its hours × the blended rate.
- Bed counts must be whole numbers: yes.
- Temp workers may be fractional: yes.
- At zero hours, the blended rate is 0

- I used the excel solver for this problem.

## Validation rules

- ABS(beds − 10/20/30) <= 0 beds
- ABS(profit_total − 42762) <= $1
- ABS(labor_hrs_t at q=1 − 99.0) <= .01 hours
- Every constraint check is TRUE; no error cells.
- Every calculated cell contains a formula, not a pasted value.
- Standalone crossing (last q before MC_x first exceeds price_x): ABS(crossing − 10 / 10 / 6) <= 1 bed

## Outputs

- `q_tomato`, `q_carrot`, `q_mesclun`, `beds_total` — the optimal mix
- `profit_total` — season profit
- `labor_hrs_t`, `labor_hrs_c`, `labor_hrs_m`, `total_hrs`, `perm_used`, `temp_hrs`, `temp_workers`, `labor_cost`, `blended_rate`
- `revenue_x`, `fert_cost_x`, `labor_cost_x` for each crop
- `VC_x(q)`, `MC_x(q)`, `AVC_x(q)` schedules and `cross_t`, `cross_c`, `cross_m`
- `all_checks` — TRUE when every validation rule passes

## Audit findings

| Check | What I found | What it would have caught |
|---|---|---|
| q = 1 by hand: 1 × 2.5 × 36 × 1.10 | Model shows 99.0 hours; hand value 99.0 | "A dropped exponent, which is the single most common structural defect and invisible downstream" (Stage 2 page) |
| Solver from 20/0/0 and from 0/0/0 | Both returned 10/20/30 and $42,761.66 | "A local optimum masquerading as the answer" (Stage 2 page) |
| Check figures | Beds 10/20/30; profit $42,761.66 against $42,762 (tolerance $1) | "Everything else, in aggregate" (Stage 2 page) |
| Break a check on purpose: price_t 8800 → 9800 (not saved) | Profit check turned FALSE; restored to 8800, back to TRUE | Functions are responding to new parameter values |
| Farm Profit Lab cross-check at 10/20/30 | Lab labor hours 5,277 vs model 5,277.2; lab labor cost $104,118 vs model $104,118; lab profit $42,762 vs model $42,761.66; lab "+1 tomato bed" −$591 | Functions don't have obvious bugs |
| Standalone P = MC crossings | Schedules sheet: tomatoes 10, carrots 10, mesclun 6 (cross_t / cross_c / cross_m), within ±1 of 10 / 10 / 6 | Incorrect data entry |
| Tomato MC dip (noted for Stage 3) | Tomato MC falls from $7,661 at q = 5 to $4,906 at q = 6; carrots dip at 16 → 17, mesclun at 13 → 14 | Not explained here; Stage 3 |
