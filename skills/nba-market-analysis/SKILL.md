---
name: nba-market-analysis
description: Translate an NBA thesis into moneyline, spread, or game-total logic for the launch-core scope. Use after the NBA game read is built and before the final edge and gate assessment.
---

# NBA Market Analysis

Read `../../sports/nba/markets.md` and `../../core/edge-quality.md`.

## Workflow
1. Match the NBA thesis to the selected market.
2. Check whether the same logic really supports that market.
3. Keep props outside the core launch flow unless explicitly handled as restricted secondary scope.
4. Make the market case concise and operational.

## Return
- market-specific NBA logic
- reasons the market fits
- reasons the market may be a poor translation of the read
