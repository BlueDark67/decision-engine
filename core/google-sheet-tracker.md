# core/google-sheet-tracker.md

## CONFIGURATION
spreadsheet_id: [SPREADSHEET_ID_HERE]

This is the only place to change the ID. All sheet references below use this value.
To migrate to a new spreadsheet, change only this value.

## Objective
Define the fixed Google Sheets tracker used by the system for daily batch intake and final entry tracking.

## Fixed tracker
- title: `Decision Engine - Sports Betting Tracker`
- spreadsheet id: use `CONFIGURATION.spreadsheet_id`
- spreadsheet url: derive from `CONFIGURATION.spreadsheet_id`

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

### Expiry rule
At the start of every batch session, the agent must check and apply this rule:

- if `status = candidata`
- and `recheck_window` timestamp has passed
- and no promotion has occurred

then set `status = expirada` on the next batch sync.

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

### Required-vs-optional classification
All `Base_Analises` fields must be classified as `[REQUIRED]` or `[OPTIONAL]`.

Field classification:
- `[REQUIRED]` `candidate_id`
- `[OPTIONAL]` `batch_id`
- `[OPTIONAL]` `received_at`
- `[OPTIONAL]` `games_date`
- `[OPTIONAL]` `source`
- `[OPTIONAL]` `raw_pick_text`
- `[REQUIRED]` `sport`
- `[OPTIONAL]` `competition`
- `[REQUIRED]` `event`
- `[OPTIONAL]` `kickoff`
- `[REQUIRED]` `market`
- `[REQUIRED]` `side`
- `[OPTIONAL]` `prop_player`
- `[OPTIONAL]` `prop_type`
- `[OPTIONAL]` `prop_line`
- `[OPTIONAL]` `prop_side`
- `[OPTIONAL]` `prop_book`
- `[OPTIONAL]` `prop_context_notes`
- `[OPTIONAL]` `analysis_mode`
- `[REQUIRED]` `data_quality`
- `[REQUIRED]` `edge_quality`
- `[REQUIRED]` `risk_load`
- `[REQUIRED]` `quick_verdict`
- `[OPTIONAL]` `odd_min`
- `[OPTIONAL]` `odd_max`
- `[REQUIRED]` `current_price`
- `[OPTIONAL]` `price_timestamp`
- `[OPTIONAL]` `price_status`
- `[OPTIONAL]` `key_supporting_factors`
- `[OPTIONAL]` `red_flags`
- `[OPTIONAL]` `checks_before_entry`
- `[OPTIONAL]` `what_could_change`
- `[OPTIONAL]` `recheck_window`
- `[OPTIONAL]` `flow_status`
- `[OPTIONAL]` `entry_id`
- `[REQUIRED]` `created_at`
- `[OPTIONAL]` `updated_at`

### Quick-triage write rule
In batch/quick-triage mode, the agent should only fill `[REQUIRED]` fields.

Minimum required fields (explicit):
- `event`
- `sport`
- `market`
- `side`
- `price` (write to `current_price`)
- `verdict` (write to `quick_verdict`)
- `edge_quality`
- `data_quality`
- `risk_load`
- `candidate_id`
- `created_at`

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

Required structure:
- `period` (example: `April 2025`, `All time`)
- `total_entries`
- `won_count`
- `lost_count`
- `void_count`
- `yield_percentage`
- `roi_percentage`
- `entries_by_sport` (football / nba / f1 breakdown)
- `avg_odds`
- `best_streak`
- `worst_streak`

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

## Controlled values
### `price_status`
- `inside_range`: current market price is within the acceptable range identified in analysis
- `outside_range`: price has moved outside acceptable range and edge may be gone
- `not_checked`: price was not verified at analysis time
- `expired`: analysis validity window has passed and current price status is unknown

### `result_status`
- `won`
- `lost`
- `void`
- `half_won`
- `half_lost`
- `pending`

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

## Result Entry Mode
Trigger:
- `Resultado: [event] [result]`

Workflow:
1. Find the matching row in `Base_Entradas` by event name plus date.
2. Update `result_status` using controlled values.
3. If P&L fields exist in the tracker, calculate and update them.
4. Update `updated_at` after result writeback.
