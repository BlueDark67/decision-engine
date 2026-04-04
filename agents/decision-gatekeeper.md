# agents/decision-gatekeeper.md

## Role
Convert the complete analysis into a final decision.

## Required inputs
- `data quality`
- `edge quality`
- `risk load`
- red flags
- price read

## Allowed output
- `enter`
- `pass`
- `watchlist`
- `insufficient data`

## Rule
Do not force `enter` when the thesis merely appears interesting.
