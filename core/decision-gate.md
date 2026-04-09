# core/decision-gate.md

## Objective
This document defines the system's final gate.

## Allowed outputs
- `enter`
- `enter_reduced`
- `enter_conditional`
- `pass`
- `watchlist`
- `insufficient_data`

## Red flag severity model
Each red flag must be tagged with one severity:

- `critical`: thesis-breaking issue that invalidates entry readiness
- `major`: high-impact issue that materially weakens confidence
- `minor`: non-blocking issue that requires caution and monitoring

## Hard-rule precedence (apply in this order)
1. `insufficient_data` overrides all other outcomes when `data_quality = insufficient`.
2. `pass` overrides remaining outcomes when any critical veto is active.
3. `watchlist` ceiling applies when major-flag veto is active.
4. Entry-family outcomes (`enter`, `enter_reduced`, `enter_conditional`) are evaluated only after veto checks.

## Automatic veto rules
- Any `critical` red flag forces `pass` regardless of edge, data, or risk.
- Two or more `major` red flags force `watchlist` maximum and block all entry-family outcomes.

## Hard decision rules
### `insufficient_data`
Use when:

- `data_quality = insufficient`

### `pass`
Use when any of the following is true:

- `edge_quality = none`
- `risk_load = extreme`
- red flags contain at least one `critical`

### `watchlist`
Use only when all of the following are true:

- `edge_quality` is at least `marginal`
- `data_quality` is at least `weak`
- `risk_load` is at most `high`
- no `critical` red flag exists
- major red flag count is below 2

### `enter` (base full-stake)
Use only when all of the following are true:

- `data quality` is `strong` or `usable`
- `edge quality` is `clear`
- `risk load` is `low`, `medium`, or `high`
- red flag condition is satisfied: total red flag count is below 2, or no red flag has severity `critical`
- no active veto rule applies

### `enter_reduced`
Use when base `enter` conditions are met and at least one of these triggers is true:

- `risk_load = high`
- exactly one non-critical red flag is present

Stake note requirement:
- output must include an explicit note recommending 50% of normal stake.

### `enter_conditional`
Use when base `enter` conditions are met but a final pre-event confirmation is still pending.

Mandatory field:
- `condition`: a single explicit condition that must be confirmed before kick-off/tipoff/race start.

If the condition is not confirmed in time:
- downgrade to `watchlist` or `pass` according to current edge and risk state.

## Tie-break and discipline rules
When multiple non-veto outcomes are technically possible, choose the most conservative one:

- prefer `enter_reduced` over `enter` when its trigger is active
- prefer `enter_conditional` over `enter` when confirmation is pending
- prefer `watchlist` over entry-family outcomes when confirmation quality is borderline

## Intake template addendum: red flag severity fields
The intake/red-flag payload must include:

- `red_flags[]`
- `red_flags[].label`
- `red_flags[].severity` (`critical` | `major` | `minor`)
- `red_flags[].evidence`
- `red_flags[].status` (`open` | `resolved`)

## Legacy compatibility note
If an external module still uses `insufficient data` (with space), map it to `insufficient_data` at gate time.
