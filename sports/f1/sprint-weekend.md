# sports/f1/sprint-weekend.md

## Objective
Define the sprint-weekend workflow variant, where reduced preparation time changes evidence quality and market confidence.

## Sprint weekend schedule
1. FP1
2. Sprint Qualifying
3. Sprint Race
4. Qualifying
5. Race

## Structural rule
Sprint weekends are not equivalent to standard weekends. Session sequencing and reduced practice data require stricter evidence handling.

## Timing-mode split
### Sprint Qualifying mode
Treat Sprint Qualifying as a separate timing mode from main Qualifying.

Required inputs:
- FP1 one-lap indicators
- setup confidence notes
- tyre warm-up behavior by team
- circuit evolution context

Data quality ceiling:
- `usable` max

Explicit rule:
- Sprint-weekend qualifying has less prep data, therefore `data_quality` cannot exceed `usable`.

### Sprint Race mode
Markets supported:
- winner
- podium
- H2H

Required inputs:
- Sprint Qualifying order
- short-run tyre behavior observed in FP1/SQ context
- overtaking profile for the circuit
- incident and Safety Car context for sprint distance

Data quality ceiling:
- `usable` max, due to reduced long-run evidence.

## Main Qualifying mode (after sprint sessions)
Use sprint evidence as contextual input, not as a full substitute for standard multi-practice preparation.

## Main Race mode
### How sprint results inform race analysis
Use sprint outputs to update:
- tyre degradation direction by team
- race-pace reference under live conditions
- overtaking feasibility and dirty-air sensitivity
- setup confidence and strategy flexibility

### Caution rule
Do not overfit race projections to sprint finishing order alone; blend sprint evidence with penalties, weather, and race-length strategy context.
