---
name: f1-market-analysis
description: Translate a Formula 1 thesis into market-specific logic for qualifying H2H, race H2H, top-6, top-10, and selective outright markets. Use after the F1 weekend read is built and the timing mode is already fixed.
---

# F1 Market Analysis

Read `../../sports/f1/markets.md` and `../../core/edge-quality.md`.

## Workflow
1. Match the F1 thesis to the selected market.
2. Check whether the timing mode supports that market call.
3. Raise the bar for winner and podium markets.
4. Make the market logic explicit instead of assuming pace alone is enough.

## Return
- market-specific F1 logic
- key supports
- key market risks
