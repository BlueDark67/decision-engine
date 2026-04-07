---
name: nba-prop-market-analysis
description: Translate an NBA player prop thesis into over/under market logic for supported restricted-scope props. Use after the prop read is built and before final edge and gate assessment.
---

# NBA Prop Market Analysis

Read `../../sports/nba/props-markets.md`, `../../core/edge-quality.md`, and `../../core/decision-gate.md`.

## Workflow
1. Match the prop thesis to the exact over/under market.
2. Check whether the current line and price still fit the thesis.
3. Validate combo props at component level before accepting the combo.
4. Make the market case concise and operational.

## Return
- prop-specific market logic
- reasons the line fits
- reasons the price or line may already be gone
