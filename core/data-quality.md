# core/data-quality.md

## Objective
`Data Quality` measures the robustness of the available inputs.

## Evaluated dimensions
- completeness
- freshness
- adequacy to the market
- coverage strength
- context stability

## Scale
### `strong`
- central inputs are present
- data is recent
- coverage is adequate for the market
- there are few material gaps

Objective threshold (all conditions required):
- official lineup confirmed
- 3 or more recent H2H references available
- league-average baseline stats available and coherent with the target market

### `usable`
- the base is sufficient to work with
- there are some controlled gaps
- it still allows a disciplined conclusion

Objective threshold (all conditions required):
- lineup is probable but not officially confirmed
- 2 or more recent H2H references available
- basic market-relevant stats available

### `weak`
- there are relevant gaps
- freshness is doubtful
- coverage is inadequate for part of the thesis

Objective threshold (any one condition is enough):
- lineup is uncertain
- only 1 H2H reference is available
- stats come from a weak-coverage environment for the selected market

### `insufficient`
- central inputs are missing
- freshness is too weak
- it is impossible to support responsible analysis

Objective threshold (all conditions required):
- no lineup information
- no H2H reference
- stats unavailable or unreliable for the selected market

## Practical rules
- strong data does not imply strong edge
- usable data does not prevent `enter`, but it requires added caution
- weak data increases the weight of `watchlist` and `insufficient data`

## Football league-tier ceiling rule
For football setups, league coverage tier constrains the maximum reachable `data quality` rating.

Classification source:
- `sports/football/league-registry.md`

Operational mapping source:
- `sports/football/coverage-modes.md`

Ceiling policy:
- `strong-stat-coverage` can reach `strong`
- `moderate-stat-coverage` caps at `usable`
- `weak-stat-coverage` caps at `weak`
- `no-stat-coverage` forces `insufficient`

If market-specific evidence is weaker than league-tier baseline, apply the weaker rating.
