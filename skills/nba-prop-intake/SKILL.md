---
name: nba-prop-intake
description: Normalize an NBA player prop request before deeper analysis. Use when the request involves `PTS`, `AST`, `REB`, `PA`, `PR`, `PRA`, or `3PM` over/under and the player, line, or pricing context needs to be made explicit.
---

# NBA Prop Intake

Read `../../AGENTS.md`, `../../core/input-standard.md`, and `../../sports/nba/props-overview.md`.

## Workflow
1. Extract player, event, prop type, side, line, price, price timestamp, and tipoff.
2. Keep missing fields explicit instead of guessing.
3. Flag whether the request fits the supported prop families.
4. Pass a clean prop packet to the next step.

## Return
- normalized prop request packet
- missing or ambiguous fields
- supported prop family or unsupported scope note
