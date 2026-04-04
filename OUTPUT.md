# OUTPUT.md

## Mandatory rule
Whenever the task involves bet analysis, this format must be followed unless the user explicitly instructs otherwise.

## Required final schema
Every final response must include these fields:

1. `Event`
2. `Sport`
3. `Market`
4. `Side`
5. `Current Price`
6. `Analysis Mode`
7. `Data Quality`
8. `Edge Quality`
9. `Risk Load`
10. `Key Supporting Factors`
11. `Red Flags`
12. `Verdict`
13. `Why This Verdict`
14. `What Could Change The Verdict`
15. `Stability / Confidence Note`

## Base template
```md
## Event
[event]

## Sport
[sport]

## Market
[market]

## Side
[side or selection]

## Current Price
[price and timestamp, if available]

## Analysis Mode
[mode used]

## Data Quality
[strong | usable | weak | insufficient]

## Edge Quality
[clear | marginal | unclear | none]

## Risk Load
[low | medium | high | extreme]

## Key Supporting Factors
- [factor 1]
- [factor 2]
- [factor 3]

## Red Flags
- [red flag 1]
- [red flag 2]

## Verdict
[enter | pass | watchlist | insufficient data]

## Why This Verdict
[short disciplined explanation]

## What Could Change The Verdict
- [trigger 1]
- [trigger 2]

## Stability / Confidence Note
[short note]
```

## Output rules
- `Verdict` must reflect the gate, not intuition alone.
- `Data Quality`, `Edge Quality`, and `Risk Load` must appear separately.
- `What Could Change The Verdict` is mandatory for `watchlist`.
- `Stability / Confidence Note` is mandatory in every case.
