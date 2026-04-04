# core/decision-gate.md

## Objective
This document defines the system's final gate.

## Allowed outputs
- `enter`
- `pass`
- `watchlist`
- `insufficient data`

## Operating rules
### `enter`
Use when:

- `data quality` is `strong` or `usable`
- `edge quality` is `clear`
- `risk load` is `low` or `medium`
- there are no unresolved critical red flags
- the thesis remains compatible with the current price

### `pass`
Use when:

- the read exists, but the edge does not compensate
- the price is no longer good
- internal contradiction is relevant
- the risk is too high for the available edge

### `watchlist`
Use when:

- the thesis may become valid
- but important confirmations are still missing
- and it is reasonable to wait for an objective trigger

Requirement:
- define what needs to change for the setup to move up or down through the gate

### `insufficient data`
Use when:

- the information base does not support responsible analysis
- central inputs are missing
- or the coverage is too weak for the market in question

## Preference rule
When in doubt between `enter` and `watchlist`, prefer `watchlist`.
When in doubt between `watchlist` and `insufficient data`, decide based on the realistic probability that the missing inputs will be resolved in time.
