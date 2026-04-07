# sports/nba/workflow.md

## Main workflow
This file governs the NBA core game-market flow.

1. Define event, market, side, and price.
2. Audit the injury report, projected starters, and rotation context.
3. Assess rest, travel, and back-to-back status.
4. Build the matchup read.
5. Translate it into moneyline, spread, or total.
6. Assess `data quality`, `edge quality`, and `risk load`.
7. Audit red flags.
8. Pass through the decision gate.

## Baseline factors
- availability
- expected minutes for key pieces
- bench depth
- pace
- shot profile
- rebounding
- turnover pressure
- rest edge

## Red flags
- outdated injury report
- poorly defined minutes restriction
- important role change not addressed
- very short sample dominating the thesis
- narrative without matchup support

## Props routing rule
If the market is a player prop, switch to the dedicated props workflow instead of using this core game-market flow.
