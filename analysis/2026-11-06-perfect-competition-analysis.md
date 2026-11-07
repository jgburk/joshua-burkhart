---
type: analysis
engagement: perfect-competition
capability: marginal-analysis
date: 2026-11-06
brief: docs/briefs/perfect-competition-brief.md
model: capabilities/marginal-analysis/model.xlsx
---

# Perfect competition — analysis

<!-- TODO: One to two pages, in your words. Headings state the finding. Cite cells. The notes below are workbook values, not conclusions; say "finish" when done and the assistant removes them. -->

## TODO: the finding on where the money crop stops

<!-- TODO. Evidence:
Revenue per bed: Model!B19 $8,800; B24 $2,094; B29 $2,700. Tomato beds: Model!B35 10; cap Model!B18 20.
Tomato MC: Schedules!D15 $8,248.59 at bed 10; Schedules!D16 $9,390.72 at bed 11. P - MC: Analysis!H5 $551.41 last bed; Analysis!J5 -$590.72 next bed. Farm Profit Lab: -$591 (Analysis!B58).
Plan hours: Model!B44 5,277.22, against owner hours Model!B10 720.
Plant-alone MC against price: carrots above at beds 11-16, below at 17-20; mesclun above at 7-13, below at 14-30 (Schedules columns D and F). First crossings: Analysis!C26:C28 10 / 10 / 6. Refer to the figure in your text.
-->

![Tomato marginal cost against price](figures/2026-11-06-perfect-competition-tomato-mc.png)

## TODO: the finding on which constraints bind and what relaxing each is worth

<!-- TODO. Evidence:
Constraint table: Analysis!A11:G16 (used, limit, slack, status, value of one more unit).
Carrots: MC at cap Schedules!D50 $1,688.95; P - MC Analysis!H6 $405.05; next bed Analysis!J6 $352.49.
Mesclun: MC at cap Schedules!D85 $2,420.10; P - MC Analysis!H7 $279.90; next bed Analysis!J7 $246.47.
Scenario rows, profit change in column U: 42 carrot cap +1 $352.49; 43 carrot cap +4 $1,075.85; 44 mesclun cap +1 $246.47; 45 mesclun cap +4 $779.33; 46 both +2 $1,109.51; 47 both +10 $1,138.83 at 10/23/31; 48 tomato cap +1 $0; 49 beds +1 $0; 41 temp workers +1 $0; 40 temp workers -1 -$551.41 at 9/20/30.
Add your own Solver re-solve here: where you read the number, and whether it matched.
-->

## TODO: the finding on why marginal cost falls

<!-- TODO. Evidence, Analysis!A20:J22. Refer to the figures in your text.
Tomatoes: bed 4 / 5 / 6 hours added 167.71 / 197.65 / 231.91; MC $6,703.12 / $7,660.86 / $4,906.28; temp hours in bed 5: 4.73.
Carrots: bed 16 / 17 / 18 hours added 60.83 / 63.46 / 66.19; MC $2,552.10 / $1,670.90 / $1,589.14; temp hours in bed 17: 56.03.
Mesclun: bed 13 / 14 / 15 hours added 60.72 / 62.14 / 63.59; MC $2,988.40 / $2,522.58 / $1,983.96; temp hours in bed 14: 29.67.
Rates: Model!B11 perm_rate $34.72; Model!B15 temp_rate $17.36.
-->

![Carrot marginal cost against price](figures/2026-11-06-perfect-competition-carrot-mc.png)

![Mesclun marginal cost against price](figures/2026-11-06-perfect-competition-mesclun-mc.png)

## TODO: the finding on whether each crop would make money alone

<!-- TODO. Evidence, Analysis!A26:O30.
Best plant-alone q and profit after the $20,000: tomatoes 10, $6,172.77 (G26); carrots 20, -$16,488.92 (G27); mesclun 30, -$11,922.19 (G28).
At plan beds, P - AVC / P - ATC: tomatoes $2,617.28 / $617.28; carrots $175.55 / -$824.45; mesclun $269.26 / -$397.41 (M26:N28).
Contribution in the plan: O26 $33,143.42; O27 $13,682.27; O28 $15,935.98; O29 $62,761.66; less fixed cost O30 $42,761.66.
-->

## TODO: the finding on the Stage 1 hypothesis

<!-- TODO. Evidence:
Brief: 20 / 20 / 24, all 64 beds, mesclun as the crop to reduce (docs/briefs/perfect-competition-brief.md).
Model: Model!B35:B38 10 / 20 / 30, 60 beds; Model!B63 $42,761.66.
Brief's mix held fixed, Analysis row 53: 14,547.81 hours; 9.60 temp workers against a limit of 4; feasible FALSE; profit -$49,906.13.
-->

## TODO: the limitations

<!-- TODO. Evidence:
Whole-worker seasons: plan held at 10/20/30, Analysis row 52, $21,880; re-solved, row 51, 10/19/28 at 2.99 workers, $41,586.
Non-field owner pay ($25,000) is outside profit_total: Analysis row 50, plan unchanged, $17,761.66.
Scenario plans in Analysis!M:O come from an exhaustive search over whole-bed mixes, not Solver.
-->
