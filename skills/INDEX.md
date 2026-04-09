# Skills Index

| Skill | Trigger | Purpose |
|-------|---------|---------|
| freshness-and-coverage-audit | Step 2 of every analysis (mandatory) | Verify data is current and sources are valid |
| recheck | `Recheck:` [candidate_id] | Re-analyse a watchlist candidate near event time |
| post-game-review | `Review:` [event] | Assess verdict accuracy after the event |
| pre-bet-intake | Start of analysis when inputs are raw | Normalize event, market, side, price, timing, and objective |
| data-quality-rater | After intake/input audit | Rate data quality as strong, usable, weak, or insufficient |
| edge-quality-rater | After market evaluation | Rate edge quality as clear, marginal, unclear, or none |
| risk-load-rater | After edge quality | Rate uncertainty and fragility as low/medium/high/extreme |
| decision-gate | Final stage before output | Convert analysis into the allowed gate verdict |
| final-output-formatter | Final response formatting stage | Render output in required schema and field order |
| daily-batch-tracker-sync | `Análises do dia:` ... `Abraço` | Split candidates, run quick triage, and sync tracker |
| entry-batch-promotion | `Entradas feitas:` | Promote confirmed entries into Base_Entradas |
| football-match-analysis | Football event analyses | Build football thesis with coverage-aware logic |
| football-market-analysis | Football market translation | Convert thesis into football market-specific logic |
| nba-game-analysis | NBA game market analyses | Build NBA game thesis for core markets |
| nba-prop-analysis | NBA player props | Build restricted-scope prop thesis |
| f1-weekend-analysis | F1 analyses | Build F1 thesis with timing-mode discipline |
| f1-market-analysis | F1 market translation | Convert F1 thesis into market-specific logic |
