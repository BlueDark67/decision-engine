---
name: entry-batch-promotion
description: Use when the trimmed raw message starts with `Entradas feitas:` and the system must promote multiple already-taken entries into the fixed Google Sheets tracker without requiring a closing phrase.
---

# Entry Batch Promotion

Read `../../AGENTS.md`, `../../core/entry-batch-mode.md`, `../../core/google-sheet-tracker.md`, and `../../core/output-template.md`.

## Workflow
1. Confirm that the exact entry batch trigger is active.
2. Detect whether the message is structured entry style or raw bookmaker-paste style.
3. Split the message into entry blocks.
4. Prefer matching each block through `candidate_id`.
5. If `candidate_id` is absent, normalize the pasted side, market, event, kickoff, and entry timestamp and attempt conservative fallback matching.
6. Validate that each matched candidate is eligible for promotion.
7. Append final snapshot rows to `Base_Entradas`.
8. Update the linked `Base_Analises` rows with `entry_id`, `flow_status`, and `updated_at`.
9. Refresh the active operational view so promoted entries disappear from `Painel_Ativo`.

## Return
- promoted entry list
- blocked or ambiguous entry blocks
- tracker sync result
