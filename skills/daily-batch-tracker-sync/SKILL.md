---
name: daily-batch-tracker-sync
description: Use when the trimmed raw message starts with `Análises do dia:` and ends with `Abraço`, and the system must split the list into candidate picks, run quick triage, and sync them to the fixed Google Sheets tracker without creating new files.
---

# Daily Batch Tracker Sync

Read `../../AGENTS.md`, `../../core/daily-batch-mode.md`, `../../core/google-sheet-tracker.md`, `../../core/input-standard.md`, and `../../core/output-template.md`.

## Workflow
1. Confirm that the exact batch trigger is active.
2. Preserve the raw message and build a batch envelope.
3. Split each bullet line into one candidate packet.
4. Run normal intake and core evaluation candidate by candidate in quick-triage mode.
5. Append or update rows in the fixed Google Sheets tracker.
6. Promote to `Base_Entradas` only when a later recheck produces a valid final entry.

## Return
- batch id
- normalized candidate list
- tracker sync plan or tracker sync result
- candidates that need later recheck
