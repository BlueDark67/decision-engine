---
name: recheck
description: Re-analyse a watchlist candidate near event time. Use when the trigger starts with `Recheck:` and includes a `candidate_id` or event identifier that should be refreshed before a final gate decision.
---

# Recheck

Read `../../AGENTS.md`, `../../core/daily-batch-mode.md`, `../../core/google-sheet-tracker.md`, `../../core/data-quality.md`, `../../core/edge-quality.md`, and `../../core/decision-gate.md`.

## Input
- `candidate_id` (preferred)
- or `event` name when `candidate_id` is unavailable

## Workflow
1. Retrieve the original candidate row from `Base_Analises`.
2. If `candidate_id` is missing, match conservatively by event and timing context.
3. Re-run the required sequence:
   - freshness-audit
   - data-quality
   - edge-quality
   - decision-gate
4. Compare the updated verdict against the original stored verdict.
5. Produce a change classification and reason.

## Output
- updated verdict
- original verdict
- `verdict_change`: `maintained` | `upgraded` | `downgraded`
- reason for verdict change
- updated fields to sync back to tracker
