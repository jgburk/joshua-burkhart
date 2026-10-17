---
type: spec
capability: marginal-analysis
engagement: perfect-competition
date: 2026-10-16
status: draft            # draft | built | audited
built_with: "<!-- TODO: tool used to build model.xlsx -->"
---

# Marginal analysis — model specification

## Purpose

This model decides how many beds to plant for each crop, in order to maximize profits.

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

<!-- TODO: each sheet or region and what it is for. -->

## Calculation logic

Labor(q) = q × hrs/wk/bed × 36 × (1 + dim)^q
max_temp_workers=4

## Conventions

- The $20,000 is a fixed cost.
- 720 hours are used first owner's.
- Each crop's labor cost = its hours × the blended rate.
- Bed counts must be whole numbers: yes.
- Temp workers may be fractional: yes.
- At zero hours, the blended rate is 0

## Validation rules

- ABS(beds − 10/20/30) <= 0 beds
- ABS(profit_total − 42762) <= $1
- ABS(labor_hrs_t at q=1 − 99.0) <= .01 hours
- Every constraint check is TRUE; no error cells.

## Outputs

<!-- TODO: each result the model reports, by name. -->

## Audit findings

<!-- Added after the build: for each check, what you checked, what you found, what you did. -->
