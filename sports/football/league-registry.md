# sports/football/league-registry.md

## Objective
Pre-classify football competitions by statistical coverage strength so analysis mode and data-quality ceilings are deterministic.

## Strong Statistical Coverage
- Premier League (ENG)
- La Liga (ESP)
- Bundesliga (GER)
- Serie A (ITA)
- Ligue 1 (FRA)
- Champions League (UEFA)
- Europa League (UEFA)
- Primeira Liga (POR)
- Eredivisie (NED)

## Moderate Statistical Coverage
- Championship (ENG)
- Liga Portugal 2 (POR)
- Serie B (ITA)
- 2. Bundesliga (GER)
- Ligue 2 (FRA)
- Eerste Divisie (NED)
- Scottish Premiership (SCO)
- Belgian Pro League (BEL)
- Austrian Bundesliga (AUT)
- Super Lig (TUR)

## Weak Statistical Coverage
- Lower national divisions with unstable public data depth
- Regional and semi-professional leagues
- Youth or reserve competitions
- Early-round domestic cups with heavy rotation and sparse event data
- Newly formed or low-liquidity competitions without reliable historical baselines

## Registry usage rule
- If a league is listed here, use its tier as the default coverage mode.
- If a league is not listed, classify conservatively as `moderate-stat-coverage` until evidence supports upgrading or downgrading.
- Coverage tier must be cross-checked with live data freshness and market adequacy before final rating.
