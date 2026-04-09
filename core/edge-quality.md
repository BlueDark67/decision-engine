# core/edge-quality.md

## Objective
`Edge Quality` measures the clarity of the perceived advantage relative to the current price.

## Evaluated dimensions
- alignment between thesis and market
- number of independent supports
- sensitivity to price
- robustness of the read

## Scale
### `clear`
- several independent supports
- the market truly appears misaligned
- the thesis does not collapse under a small revision of the noise

Objective threshold:
- 3 or more independent factors converge in the same direction
- absolute market divergence is greater than 5% versus model fair price

### `marginal`
- there is some value argument
- but the advantage is narrow or price-sensitive

Objective threshold:
- 2 independent factors and market divergence between 2% and 5%, inclusive
- or 3 or more factors with market mostly aligned to model (divergence below 2%)

### `unclear`
- the read exists, but the advantage is not distinct
- the price may already reflect most of the thesis

Objective threshold:
- single-factor thesis only
- or conflicting directional signals between factors

### `none`
- no identifiable advantage
- or the price is clearly inadequate

Objective threshold:
- no identifiable edge after factor review
- or market is correctly priced to model and context

## Divergence definition
Use absolute divergence between model fair probability and market implied probability:

`abs(model_prob - market_implied_prob)`

Apply the thresholds above directly to this absolute value.

## Practical rules
- a good sports read can still have weak `edge quality`
- `enter` normally requires `clear`
- `marginal` tends to push toward `pass` or `watchlist`
