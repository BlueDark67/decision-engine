# core/risk-load.md

## Objective
`Risk Load` measures the weight of uncertainty and thesis fragility.

## Evaluated dimensions
- event volatility
- dependence on still-unstable inputs
- internal contradictions
- market fragility
- sport-specific contextual risk

## Scale
### `low`
- the context is stable
- few variables remain unresolved
- the thesis is robust

Objective threshold (all conditions required):
- no correlated bets active
- event context is neutral
- data quality rated `strong`

### `medium`
- there is real risk, but it is manageable
- still compatible with `enter` if the edge is clear

Objective threshold:
- 1 correlated bet active
- or event context is elevated (for example derby, cup final, structurally high-pressure spot)

### `high`
- there are multiple sources of fragility
- caution is required
- favors `pass` or `watchlist`

Objective threshold (any one condition is enough):
- 2 or more correlated bets active
- data quality rated `weak`
- significant lineup uncertainty

### `extreme`
- contextual chaos or uncertainty is too high
- compatible with `pass` or `insufficient data`, and almost never with `enter`

Objective threshold (any one condition is enough):
- 3 or more correlated bets active
- data quality rated `insufficient`
- key player status unknown and thesis-critical

## Central rule
`Risk Load` can override an apparently attractive edge when the fragility of the read is too high.
