# core/google-sheet-tracker.md

## Objective
Define the fixed Google Sheets tracker used by the system for daily batch intake and final entry tracking.

## Fixed tracker
- title: `Decision Engine - Sports Betting Tracker`
- spreadsheet id: `1TuqcKcaFkOyZF9iAt5lOXSaTDDYC_voHnim4d-m1Dew`
- spreadsheet url: `https://docs.google.com/spreadsheets/d/1TuqcKcaFkOyZF9iAt5lOXSaTDDYC_voHnim4d-m1Dew/edit?usp=drivesdk`

## Access surface
This tracker must be accessed through the connected Google Drive / Google Sheets capabilities.

## Non-negotiable file rule
- reuse this same spreadsheet
- do not create a new spreadsheet for each day
- do not create alternative tracker files unless the user explicitly requests a replacement

## Sheet roles
### `Painel_Ativo`
Operational working view for open candidates and near-term items.

Use it for:
- current open candidates
- price checks
- recheck timing
- active flow status
- quick prop context when the open item is an NBA player prop

This page is operational, not historical. It may be rewritten from the current active set.

When the active item is an NBA player prop, the panel should also carry:
- `prop_player`
- `prop_type`
- `prop_line`
- `prop_side`
- `prop_book`

### `Base_Analises`
Primary historical table for candidate setups created from daily list intake.

One row per candidate. This is the canonical historical record for:
- raw suggestion
- quick-triage fields
- odd range
- checks before entry
- flow status
- link to final entry, when promoted

Minimum write fields:
- `candidate_id`
- `batch_id`
- `received_at`
- `games_date`
- `source`
- `raw_pick_text`
- `sport`
- `competition`
- `event`
- `kickoff`
- `market`
- `side`
- `prop_player`
- `prop_type`
- `prop_line`
- `prop_side`
- `prop_book`
- `prop_context_notes`
- `analysis_mode`
- `data_quality`
- `edge_quality`
- `risk_load`
- `quick_verdict`
- `odd_min`
- `odd_max`
- `current_price`
- `price_timestamp`
- `price_status`
- `key_supporting_factors`
- `red_flags`
- `checks_before_entry`
- `what_could_change`
- `recheck_window`
- `flow_status`
- `entry_id`
- `created_at`
- `updated_at`

### `Base_Entradas`
Historical table for final entries that were actually approved near game time.

One row per promoted entry. This page stores the final snapshot used at approval time.

Minimum write fields:
- `entry_id`
- `candidate_id`
- `batch_id`
- `sent_at`
- `event_date`
- `kickoff`
- `sport`
- `competition`
- `event`
- `market`
- `side`
- `prop_player`
- `prop_type`
- `prop_line`
- `prop_side`
- `prop_book`
- `prop_context_notes`
- `odd_entrada`
- `odd_timestamp`
- `analysis_mode`
- `data_quality`
- `edge_quality`
- `risk_load`
- `key_supporting_factors`
- `red_flags`
- `verdict_final`
- `why_this_verdict`
- `observacoes`
- `stability_note`
- `result_status`
- `updated_at`

### `Resumo_Historico`
Summary layer for counts and historical overview.

Do not use it as the primary write target for operational rows.

### `Config`
Reference page for allowed values and tracker conventions.

It should include the controlled value sets used by prop rows, especially:
- supported `prop_type` values
- supported `prop_side` values
- allowed `analysis_mode` values including `NBA props restricted scope`

## Row policy
### New daily batch
- append new candidate rows to `Base_Analises`
- assign a stable `candidate_id`
- assign a `batch_id` shared by the message batch

### Candidate re-evaluation
- update the existing `Base_Analises` row for that `candidate_id`
- keep the raw suggestion and historical identity stable
- if the market is a player prop, keep the prop identity stable across updates:
  - `prop_player`
  - `prop_type`
  - `prop_line`
  - `prop_side`

### Promotion to final entry
- append a new row to `Base_Entradas`
- assign an `entry_id`
- backfill `entry_id` into the matching `Base_Analises` row
- set `flow_status` in `Base_Analises` to `entrada_confirmada`
- update `updated_at` in the candidate row
- ensure the promoted row drops out of `Painel_Ativo` on the next active-view sync

## Snapshot rule
`Base_Entradas` is a final snapshot table.

This means:
- final odd
- final verdict
- final observations
- final stability note

should reflect the moment of approval and should not be silently rewritten by later changes in the candidate row.

For non-prop rows, the prop-specific fields should remain blank.

## Active-panel rule
`Painel_Ativo` may contain a filtered or rewritten view of non-closed candidates.

It should prioritize:
- today's and tomorrow's games
- items awaiting recheck
- items with valid odds
- candidates not yet closed

## Failure rule
If the spreadsheet cannot be found or written:

- do not create a replacement file
- do not write to a local substitute
- report the blocker clearly

## Matching rule
The tracker sync layer runs when either:

- daily batch mode is active according to `core/daily-batch-mode.md`
- entry batch mode is active according to `core/entry-batch-mode.md`

In entry batch mode, fallback matching should prefer a normalized operational tuple built from:

- event
- market
- side
- kickoff

and then use entry-time or price fields only as secondary disambiguation when needed.

If the row is an NBA player prop, fallback matching should prefer a prop-aware tuple built from:

- event
- prop_player
- prop_type
- prop_line
- prop_side
- kickoff

and then use book, entry-time, or price fields only as secondary disambiguation when needed.
