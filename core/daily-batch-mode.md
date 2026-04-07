# core/daily-batch-mode.md

## Objective
Define the disciplined operating mode for daily list intake, quick candidate triage, and tracker sync.

## Activation trigger
This mode activates only when the raw user message, after trimming outer whitespace, satisfies both conditions:

- starts with the exact string `Análises do dia:`
- ends with the exact string `Abraço`

If either boundary is missing, daily batch mode must not activate.

## Central interpretation rule
In this mode, each bullet line is a candidate setup, not a final entry.

Examples:

- `Empate anula Bayern`
- `0.5+ golos equipa Sporting`
- `Vence Fluminense`
- `Ambas marcam jogo Wrexham`
- `Jalen Brunson over 8.5 assists`

These lines are raw prompts for disciplined evaluation. They do not bypass intake, data checks, price discipline, or the decision gate.

## Batch envelope fields
When this mode activates, preserve:

- raw message
- received timestamp
- inferred games date, when available
- batch id
- one raw candidate line per bullet

Blank spacer lines should be ignored. Each candidate line must preserve the original suggestion text.

## Required processing order
1. Detect the daily batch trigger.
2. Build a batch envelope.
3. Split the message into candidate lines.
4. Normalize each candidate into an intake packet.
5. Run the normal core order for each candidate in quick-triage mode.
6. Write or update tracker rows in the fixed Google Sheets file.
7. Promote to final entry only later, after recheck near game time.

## Parsing rule
Inside the batch envelope:

- each non-empty line beginning with `-` is one candidate
- the candidate text should be preserved without inventing missing fields
- malformed lines should be kept explicit instead of silently normalized into certainty

If the candidate is clearly an NBA player prop, the intake packet should also preserve, when available:

- `prop_player`
- `prop_type`
- `prop_line`
- `prop_side`

## Quick-triage objective
The purpose of daily batch mode is not to finalize a bet immediately. It is to:

- decide whether the idea is worth tracking
- indicate whether the system broadly agrees, disagrees, or needs to wait
- define an acceptable odd range
- define what must be checked before entry

## Quick-triage discipline
Even in fast mode, the system must still:

- separate `data quality`, `edge quality`, and `risk load`
- keep missing fields explicit
- avoid narrative agreement without support
- prefer `watchlist` or `insufficient data` when the base is weak

## Price rule
A candidate may look valid in principle and still fail on price.

Therefore the quick-triage output must explicitly indicate:

- acceptable odd range
- whether the current number is still inside that range, when available
- what price movement would kill the setup

## Promotion rule
A candidate row in the tracker becomes a final entry only after a later recheck confirms:

- the market still fits the thesis
- the current price is still acceptable
- unresolved confirmations have been addressed
- the gate still supports the decision

## Write policy
- Use the fixed tracker defined in `core/google-sheet-tracker.md`.
- Never create a new daily spreadsheet.
- Never create a substitute local file if the tracker is unavailable.
- If the trigger is not active, do not write to the tracker.
- If the tracker cannot be reached, make the limitation explicit and stop the sync layer.
- When the candidate is a player prop, write the prop fields into the tracker and leave them blank for non-prop rows.

## Output policy
When this mode is active, a compact batch-processing summary is acceptable in chat, provided that the structured candidate records are written to the tracker and any later promoted final entry uses the project output schema.
