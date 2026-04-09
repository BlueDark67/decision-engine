# sports/nba/props-workflow.md

## Scope inheritance
This workflow extends core/game-workflow and `sports/nba/workflow.md`. All steps from those apply unless explicitly overridden below.

## Differences only
### Player-specific data sources
- player role and on-ball responsibility in current rotation
- projected minutes range with injury-report timestamp
- on/off context from key teammate absences/returns
- prop-family splits relevant to the selected line (`PTS`, `AST`, `REB`, `PA`, `PR`, `PRA`, `3PM`)

### Prop-specific red flags
- role appears stable in narrative but unstable in expected substitution pattern
- projected blowout materially threatens minutes tail
- line movement already captured the usage bump from injury news
- thesis depends on unsustainably hot shooting without volume support

### Prop-specific edge factors
- line-to-role mismatch relative to expected usage and touches
- minutes stability relative to the selected prop family
- matchup channel fit (rim pressure, pull-up volume, assist conversion, rebound environment)
- price sensitivity around adjacent lines in the same prop ladder

## Minutes-floor rule (hard gate)
- If `projected_minutes < 20`: set `data_quality = insufficient` for all props.
- If `projected_minutes` is between 20 and 25: set `data_quality = weak` for scoring props and `data_quality = usable` for assists/rebounds props.
- If `projected_minutes > 25`: apply normal data quality rules.

## Rule
Do not let a recent streak replace clear minutes, role, and matchup logic.
