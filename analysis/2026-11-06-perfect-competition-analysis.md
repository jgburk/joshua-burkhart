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

## Tomato Bed Limit

Tomatoes earn the most per bed ($8,800 vs $2,700 and $2,094) but only 10 of 20 beds get planted. The cost per bed increases at the 11th bed to the point that it outweighs the price.
Bed 10 costs $8,248.59 so price minus MC is $551.41.
Bed 11 would be $9,390.72 so price minus MC is -$590.72.
The model stops at 10 beds because the cost of an eleventh bed would outweigh price.

![Tomato marginal cost against price](figures/2026-11-06-perfect-competition-tomato-mc.png)

## Carrot and Mesclun Maximally Planted

Both Carrot and Mesclun were planted in 20/20 and 30/30 beds, respectively.
The price of carrot is $2,094, MC is $1,688.95
The price of mesclun is $2,700, MC is $2,420.10
The cap is what stops us from planting more of each crop.
If we planted another bed of each, Carrot would be $352.49 (+ profit) and Mesclun would be $246.47 (+ profit).
Tomato cap: 10 of 20
Total beds: 60 of 64
Temp workers 3.16 of 4
Adding more of any of them adds $0 because they are slack.

## Marginal cost falls because hours cost $17.36 from temp workers after using all the owner's hours at $34.72.

-Tomato: 5-6 ($7,661 to $4,906)
Carrots: 16-18 ($2,552 to $1,589)
Mesclun: 13-15 ($2,988 to $1,984)

1. The physical returns did not improve. The cost just decreased.
2. MC reflects all the material, supplies, and labor. What changed was the price of the wage.

![Carrot marginal cost against price](figures/2026-11-06-perfect-competition-carrot-mc.png)

![Mesclun marginal cost against price](figures/2026-11-06-perfect-competition-mesclun-mc.png)

## Only Tomato Makes Money Alone

<!-- TODO. Evidence, Analysis!A26:O30.
Best plant-alone q and profit after the $20,000: tomatoes 10, $6,172.77 (G26); carrots 20, -$16,488.92 (G27); mesclun 30, -$11,922.19 (G28).
At plan beds, P - AVC / P - ATC: tomatoes $2,617.28 / $617.28; carrots $175.55 / -$824.45; mesclun $269.26 / -$397.41 (M26:N28).
Contribution in the plan: O26 $33,143.42; O27 $13,682.27; O28 $15,935.98; O29 $62,761.66; less fixed cost O30 $42,761.66.
-->

Tomato would make money alone but Carrot and Mesclun would lose money.
The 20K isn't the issue. It's owed whether or not another bed is planted.
Price is above avc for carrot and meslcun. Each bed pays for itself with extra toward the 20K.

## Limitations

The temps are hourly. If they have to be paid for the whole season, profit for the 10/20/30 split goes down from $42,761.66 to $21,880. That means the profit number has a large variance, depending on a single factor.

## Tomato, Mesclun, Total Count Mistakes

<!-- TODO. Evidence:
Brief: 20 / 20 / 24, all 64 beds, mesclun as the crop to reduce (docs/briefs/perfect-competition-brief.md).
Model: Model!B35:B38 10 / 20 / 30, 60 beds; Model!B63 $42,761.66.
Brief's mix held fixed, Analysis row 42: 14,547.81 hours; 9.60 temp workers against a limit of 4; feasible FALSE; profit -$49,906.13.
-->

I predicted 20/20/24 vs 10/20/30 on 60 beds.
Bed 11 cost too much for tomato. So we won't plant more than 10.
I assumed all beds should be planted. That wasn't true because of the way the costs built up. 60 were best.
I also thought mesclun wouldn't be planted as much (24 vs 30) due to high fertilizer cost. this turned out to be incorrect. Mesclun's price stays above MC up to 30 beds+ in the combined plan.
