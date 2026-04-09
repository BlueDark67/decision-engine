# sports/football/special-contexts.md

## Objective
Define mandatory context adjustments for football spots where baseline market assumptions are structurally distorted.

## Neutral venue games
### Required adjustments
- remove default home-advantage assumptions
- rebalance form metrics that over-weight home/away splits
- re-evaluate pace, pressing intensity, and crowd-pressure effects

### Key checks
- travel burden for both teams
- familiarity with venue and pitch
- expected fan distribution and atmosphere neutrality

## Cup second legs
### Mandatory fields
- first_leg_result
- aggregate_score
- qualification_rules (away goals, extra time, penalties)
- what_each_team_needs (win margin, draw sufficiency, must-score scenarios)

### Required adjustments
- model game-state incentives from minute 1
- account for asymmetric urgency and late-game risk spikes
- separate pre-match edge from in-play path dependency

## Dead rubber matches
### Required adjustments
- estimate rotation likelihood for both sides
- include motivation flags for coaching objectives and player incentives
- downgrade confidence in baseline form continuity

### Motivation flags
- qualified/eliminated status already fixed
- expected minutes management
- development-focused lineup signals

## Relegation and title deciders
### Required adjustments
- mark context as elevated pressure
- increase volatility allowance for game-state swings
- reduce confidence in generic season-average assumptions

### Market-efficiency note
- these spots are often highly observed and rapidly repriced
- require stricter edge confirmation before entry-family outcomes

## Cross-context rule
If a match falls into multiple special contexts, use the most conservative interpretation for data quality and risk load.
