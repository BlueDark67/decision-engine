# sports/nba/props-overview.md

## Objective
This module covers NBA player props in restricted secondary scope.

## Supported markets
- over/under `PTS`
- over/under `AST`
- over/under `REB`
- over/under `PA`
- over/under `PR`
- over/under `PRA`
- over/under `3PM`

## Required inputs
- player
- teams
- tipoff
- prop type
- side (`over` or `under`)
- line and price
- price timestamp
- injury report with timestamp
- expected starters and rotation context
- projected role
- projected minutes
- matchup context relevant to the prop

## Central principle
For NBA props, minutes and role stability come before raw averages or recent streaks.

## Structural rule
Props remain restricted secondary scope. They require dedicated workflow and should not inherit confidence from the NBA core game-market flow.
