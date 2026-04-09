# sports/football/coverage-modes.md

Coverage classification source: see `sports/football/league-registry.md`.
Data-quality constraint source: see `core/data-quality.md`.

## Strong-Stat-Coverage
Use when:

- the competition has good statistical depth
- the relevant data exists for the market in question
- the thesis does not depend on excessively weak proxies

## Acceptable use of xG
xG-centered reasoning is acceptable only when:

- the statistical coverage is strong
- the event or team has usable xG support
- the thesis does not depend on an excessively small sample
- lineup uncertainty does not destroy the basis of the read

## Weak-Stat-Coverage
Use when:

- statistical coverage is limited
- xG is absent, delayed, or unreliable
- the market demands more than the data truly supports

## Conservative mode
In `weak-stat-coverage`, the read should rely more on:

- competitive context
- form and schedule
- availability
- tactical matchup
- market behavior

## Rule
A heavily xG-driven thesis in `weak-stat-coverage` is a red flag.

## Coverage-to-quality mapping
| league_coverage_mode | data_quality_ceiling |
| --- | --- |
| `strong-stat-coverage` | `strong` (no ceiling applied) |
| `moderate-stat-coverage` | `usable` (max) |
| `weak-stat-coverage` | `weak` (max) |
| `no-stat-coverage` | `insufficient` (forced) |

## Ceiling rule
If observed evidence suggests a better score than the coverage ceiling, keep the ceiling.
Only a justified manual override may lift a ceiling, and it must document why the market-specific data quality is structurally stronger than league baseline.
