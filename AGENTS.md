# AGENTS.md

## Purpose
This file is the entry point for the project. The project is not a programming repository. It is a structured analysis and decision-support system for sports betting.

Core system question:

> Should I enter this bet or not, and why?

## Required reading
Before producing any analysis, Codex must consult these files in this order:

1. `AGENTS.md`
2. `CONTEXTO.md`
3. `REGRAS.md`
4. `ESTILO.md`
5. `OUTPUT.md`
6. `core/system-map.md`
7. `core/input-standard.md`
8. `core/data-quality.md`
9. `core/edge-quality.md`
10. `core/risk-load.md`
11. `core/red-flags.md`
12. `core/decision-gate.md`
13. `core/output-template.md`

After that, it must consult the relevant sport-specific module:

- Football: `sports/football/`
- NBA: `sports/nba/`
- F1: `sports/f1/`

When a task matches an internal project skill, Codex must also consult the `skills/` folder.

## System type
The system was designed using a balanced approach:

- a shared core for intake, data quality, edge, risk, red flags, gate, and output
- sport-specific modules for football, NBA, and F1
- market-oriented decisions, without implementing APIs or automated data fetching

## Required operating order
No analysis may skip steps. The base order is:

1. Intake
2. Input audit
3. Data quality assessment
4. Sport-specific analysis
5. Market evaluation
6. Edge quality assessment
7. Risk load assessment
8. Red flag audit
9. Decision gate
10. Final output

## Required separations
Codex must explicitly separate:

- `data quality`: quality, freshness, and adequacy of the data
- `edge quality`: clarity and robustness of the perceived advantage
- `risk load`: weight of uncertainty, volatility, and thesis fragility

These three dimensions must never be merged.

## Sport-specific structural rules
- Football: use league-aware logic. Distinguish between `strong-stat-coverage` and `weak-stat-coverage` environments.
- Football: use xG-centered reasoning only when the environment supports it.
- NBA: keep props outside the launch core. Treat them as restricted secondary scope.
- F1: treat `pre-practice`, `post-practice`, `post-qualifying`, and `pre-race` as structurally different modes.

## Core red flags
Codex must treat any thesis as a central red flag when it is:

- too narrative-driven
- weakly supported by evidence
- strong in wording but weak in verifiable support

A weak or narrative-driven thesis without enough support must not be promoted to `enter`.

## Decision policy
The only allowed final outputs from the gate are:

- `enter`
- `pass`
- `watchlist`
- `insufficient data`

If there is structural uncertainty, missing inputs, or important contradictions, Codex must prefer `watchlist` or `insufficient data`, never force an entry.

## Consistency policy
Comparable analyses must use:

- the same reasoning chain
- the same level of rigor
- the same final output schema

If there are exceptions, they must be justified explicitly.

## Project state
This system should be treated as an editable modular foundation. If any criterion is still not fully defined, Codex must:

- make the limitation explicit
- keep the reading disciplined
- avoid inventing certainty where none exists
