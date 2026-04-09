# Decision Engine

Main entry point: see `AGENTS.md`.

## System overview
1. This repository is a Markdown-based sports betting decision-support system.
2. It is a reasoning framework, not a traditional application codebase.
3. The core question is whether to enter a bet and why.
4. The system enforces a fixed analysis pipeline from intake to final output.
5. Data quality, edge quality, and risk load are independent mandatory dimensions.
6. Supported sports are Football, NBA, and Formula 1.
7. Sport modules extend the shared core without replacing it.
8. Decision outputs are constrained to enter, pass, watchlist, or insufficient data.
9. Daily Batch Mode and Entry Batch Promotion Mode are trigger-based workflows.
10. Final responses must follow the required schema and style definitions.

## Directory map
| Folder | Purpose |
| --- | --- |
| `agents/` | Conceptual agent modules and participation order definition. |
| `core/` | Shared pipeline, governance rules, and mode/tracker policies. |
| `skills/` | Reusable workflow modules used by the agent when tasks match. |
| `skills/daily-batch-tracker-sync/` | Batch tracker synchronization workflow. |
| `skills/data-quality-rater/` | Data quality assessment workflow. |
| `skills/decision-gate/` | Final decision gate workflow. |
| `skills/edge-quality-rater/` | Edge quality assessment workflow. |
| `skills/entry-batch-promotion/` | Entry batch promotion workflow. |
| `skills/f1-market-analysis/` | Formula 1 market analysis workflow. |
| `skills/f1-mode-router/` | Formula 1 mode routing workflow. |
| `skills/f1-weekend-analysis/` | Formula 1 weekend structure analysis workflow. |
| `skills/final-output-formatter/` | Final output schema formatting workflow. |
| `skills/football-league-context/` | Football league-context workflow. |
| `skills/football-market-analysis/` | Football market analysis workflow. |
| `skills/football-match-analysis/` | Football match analysis workflow. |
| `skills/freshness-and-coverage-audit/` | Data freshness and coverage audit workflow. |
| `skills/input-completeness-check/` | Input completeness and minimum-data checks. |
| `skills/market-price-evaluator/` | Market price evaluation workflow. |
| `skills/nba-game-analysis/` | NBA game analysis workflow. |
| `skills/nba-market-analysis/` | NBA market analysis workflow. |
| `skills/nba-player-role-context/` | NBA player role/context workflow. |
| `skills/nba-prop-analysis/` | NBA prop analysis workflow. |
| `skills/nba-prop-intake/` | NBA prop intake workflow. |
| `skills/nba-prop-market-analysis/` | NBA prop market analysis workflow. |
| `skills/nba-schedule-and-rotation-context/` | NBA schedule and rotation workflow. |
| `skills/pre-bet-intake/` | Pre-bet intake standardization workflow. |
| `skills/red-flag-audit/` | Red flag auditing workflow. |
| `skills/risk-load-rater/` | Risk load assessment workflow. |
| `sports/` | Sport-specific framework modules. |
| `sports/football/` | Football-specific context, workflow, and markets. |
| `sports/nba/` | NBA-specific context, game and prop workflows, and markets. |
| `sports/f1/` | Formula 1-specific modes, workflow, and markets. |

## Quick start
### Single analysis
1. Read `AGENTS.md` and complete the startup checklist.
2. Follow the required reading order and load the correct sport module.
3. Run the core pipeline for one candidate setup.
4. Emit final output in the required schema from `OUTPUT.md` and style from `ESTILO.md`.

### Daily batch
1. Start only when the trimmed message starts with `Análises do dia:` and ends with `Abraço`.
2. Split each bullet into a candidate setup packet.
3. Run the full core pipeline per candidate.
4. Sync tracker fields using `core/google-sheet-tracker.md` rules.
5. Mark each candidate as enter, pass, watchlist, or insufficient data.
