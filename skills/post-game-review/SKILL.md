---
name: post-game-review
description: Review a completed event against the original decision quality. Use when the trigger starts with `Review:` and includes an event plus actual result for post-game learning and tracker update.
---

# Post-Game Review

Read `../../AGENTS.md`, `../../core/google-sheet-tracker.md`, `../../core/decision-gate.md`, and `../../OUTPUT.md`.

## Input
- event name
- actual result

## Workflow
1. Retrieve original verdict and key supporting factors from `Base_Analises` and `Base_Entradas`.
2. Compare the pre-event thesis with actual event outcome.
3. Evaluate both decision correctness and factor correctness.
4. Assign `review_verdict` using controlled values.
5. Write review notes and result updates back to tracker.

## review_verdict controlled values
- `correct_enter`
- `correct_pass`
- `incorrect_enter`
- `incorrect_pass`

## Output
- `review_verdict`
- learning_note
- factor-accuracy summary
- tracker update payload

## Tracker writes
- update `result_status` in `Base_Entradas`
- append/refresh `observacoes` with review learning note
