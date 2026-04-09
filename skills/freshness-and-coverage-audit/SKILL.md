---
name: freshness-and-coverage-audit
description: Assess whether available inputs are fresh enough and whether the coverage environment supports the planned reasoning. Mandatory at Step 2 of every analysis pipeline, regardless of analysis type or mode.
---

# Freshness And Coverage Audit

Read `../../core/input-standard.md`, `../../core/data-quality.md`, `../../sports/football/coverage-modes.md`, and `../../sports/f1/timing-modes.md` when relevant.

## Workflow
0. Execute this skill as mandatory Step 2 in every analysis pipeline.
1. Check whether key inputs are time-sensitive.
2. Flag stale odds, stale news, stale injuries, stale penalties, or stale lineups.
3. For football, classify the environment as `strong-stat-coverage` or `weak-stat-coverage`.
4. For F1, confirm whether the current timing mode has the inputs it needs.

## Return
- freshness issues
- coverage fit
- provisional coverage mode when relevant
- effect on data quality
