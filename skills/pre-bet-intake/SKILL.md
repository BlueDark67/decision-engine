---
name: pre-bet-intake
description: Normalize a raw betting request into a structured analysis packet for football, NBA, or Formula 1. Use when starting any analysis and the event, market, side, price, timing, or objective need to be made explicit before deeper reasoning.
---

# Pre-Bet Intake

Read `../../AGENTS.md`, `../../core/input-standard.md`, and `../../core/output-template.md`.

## Workflow
1. Extract the event, sport, market, side, current price, price timestamp, event time, and analysis objective.
2. Keep missing fields explicit instead of guessing.
3. Identify which sport module should run next.
4. Pass a clean intake packet to the next step.

## Return
- normalized request packet
- missing or ambiguous fields
- recommended next module
