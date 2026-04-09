# sports/nba/special-contexts.md

## Objective
Define structural NBA contexts that require mandatory risk and interpretation adjustments before market translation and gate output.

## Rest games and load management
### Mandatory red-flag rule
- If a star player is listed as `probable` or `questionable` with back-to-back fatigue context, tag a `major` red flag.

### Mandatory risk-load rule
- If a team is on the second night of a back-to-back, add a risk-load penalty and record it explicitly in the risk rationale.

### Required checks
- last-game minute load for core players
- travel burden between games
- coach history on late scratches and minute caps

## In-Season Tournament (IST)
### Context rule
- Motivation profiles can diverge from regular-season baseline and must be assessed explicitly.

### Mandatory note
- Some teams rest starters after IST elimination; projection must account for potential motivation drop and rotation change.

## Play-In Tournament
### Context rule
- Treat as high-stakes playoff-like context.

### Required adjustments
- shorten tolerance for experimental rotations
- increase weight of coaching matchup planning
- increase caution around foul-risk and late-game volatility

## Playoffs
### Structural adjustments
- pace generally slows relative to regular season baseline
- defensive intensity and possession value increase
- home-court impact tends to strengthen
- coaching adjustments become central to projection stability

### Factor-level adjustments
- pace factor: reduce baseline possessions unless matchup-specific evidence supports normal pace
- efficiency factor: downgrade naive regular-season efficiency carryover
- rotation factor: expect tighter rotations and higher star-minute concentration
- matchup factor: increase impact of targeted scheme counters
- market factor: require stronger edge confirmation because playoff markets are highly efficient

## Cross-context rule
If multiple special contexts apply, use the most conservative combined interpretation for `data_quality`, `edge_quality`, and `risk_load`.
