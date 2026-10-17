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

<!-- TODO: each sheet or region and what it is for. -->

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

## Outputs

Tomatoes beds	10
Carrots beds	20
Mesclun beds	30
Beds planted	60
	
LABOR	
Tomatoes labor hours	2,334.4
Carrots labor hours	983.2
Mesclun labor hours	1,959.7
Total hours	5,277.2
Owner hours used	720.0
Temp hours	4,557.2
Temp workers	3.16
Labor cost	$104,118
Blended rate	$19.73
	
FARM P&L	
Tomatoes revenue	$88,000
Tomatoes fertilizer	$8,800
Tomatoes labor cost	$46,057
Carrots revenue	$41,880
Carrots fertilizer	$8,800
Carrots labor cost	$19,398
Mesclun revenue	$81,000
Mesclun fertilizer	$26,400
Mesclun labor cost	$38,664
	
PROFIT (Solver objective)	
Profit	$42,761.66

## Audit findings

| Check | What I found | What it would have caught |
|---|---|---|
| q = 1 by hand: 1 × 2.5 × 36 × 1.10 | Model shows 99.0 hours; hand value 99.0 | A dropped exponent, which is the single most common structural defect and invisible downstream |
| Solver from 20/0/0 and from 0/0/0 | Both returned 10/20/30 and $42,761.66 | A local optimum masquerading as the answer |
| Check figures | Beds 10/20/30; profit $42,761.66 against $42,762 (tolerance $1) | Everything else, in aggregate |
