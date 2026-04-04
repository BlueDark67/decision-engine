---
name: f1-mode-router
description: Route a Formula 1 betting analysis into pre-practice, post-practice, post-qualifying, or pre-race mode. Use before any F1 thesis is built, because the acceptable claims and required inputs change with the weekend phase.
---

# F1 Mode Router

Read `../../sports/f1/overview.md` and `../../sports/f1/modes.md`.

## Workflow
1. Identify the current weekend phase.
2. Match the setup to `pre-practice`, `post-practice`, `post-qualifying`, or `pre-race`.
3. Confirm which inputs are required in that mode.
4. Downgrade the setup if the mode is wrong for the available evidence.

## Return
- F1 timing mode
- required inputs for that mode
- warning if the mode is under-supported
