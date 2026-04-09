# AGENTS.md

## STARTUP CHECKLIST (verify before any analysis)
1. [ ] AGENTS.md loaded
2. [ ] core/system-map.md loaded
3. [ ] core/intake-agent.md loaded
4. [ ] core/data-quality.md loaded
5. [ ] core/edge-quality.md loaded
6. [ ] core/risk-load.md loaded
7. [ ] core/decision-gate.md loaded
8. [ ] OUTPUT.md loaded
9. [ ] ESTILO.md loaded
10. [ ] Correct sport module loaded
11. [ ] Google Sheets tracker loaded (if batch mode)

## Purpose
This file is the entry point for the project. The project is not a programming repository. It is a structured analysis and decision-support system for sports betting.

Core system question:

> Should I enter this bet or not, and why?

For agent order, see `agents/INDEX.md`.

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
14. `core/daily-batch-mode.md`
15. `core/google-sheet-tracker.md`
16. `core/entry-batch-mode.md`

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
- an optional fixed Google Sheets operational tracker for daily candidate intake and final entry history

## Required operating order
No analysis may skip steps. The base order is:

1. Intake
2. Input audit
Step 2 of every analysis pipeline is mandatory execution of `skills/freshness-and-coverage-audit`. This step cannot be skipped regardless of analysis type or mode.
3. Data quality assessment
4. Sport-specific analysis
5. Market evaluation
6. Edge quality assessment
7. Risk load assessment
8. Red flag audit
9. Decision gate
10. Final output

When daily batch mode is active, the system must first detect the batch envelope, split it into candidate setups, and then run the same base order for each candidate.

## Required separations
Codex must explicitly separate:

- `data quality`: quality, freshness, and adequacy of the data
- `edge quality`: clarity and robustness of the perceived advantage
- `risk load`: weight of uncertainty, volatility, and thesis fragility

These three dimensions must never be merged.

## Daily batch tracker mode
For the special daily-list workflow:

- only activate it when the trimmed raw message starts with `Análises do dia:` and ends with `Abraço`
- if exact boundaries are missing but 3 or more sport-like candidate lines are detected, ask for confirmation with the defined fuzzy-trigger prompt in `core/daily-batch-mode.md`
- treat each bullet as a candidate setup, not a final entry
- reuse the fixed Google Sheets tracker defined in `core/google-sheet-tracker.md`
- never create a new daily spreadsheet
- apply quick-triage scope exactly as defined in `core/daily-batch-mode.md` (including never-skip steps and omitted deep checks)
- if candidate count is greater than 8, issue the batch-size warning and require explicit confirmation before processing all at once
- support inline odd parsing in candidate lines (`@ odd` and optional bookmaker note in parentheses), mapping odd to `price` and bookmaker note to `observacoes`
- quick triage may populate odds range, checks, and watchlist status, but final entry still requires a later recheck

## Entry batch promotion mode
For reporting one or more entries already taken:

- only activate it when the trimmed raw message starts with `Entradas feitas:`
- no closing phrase is required
- prefer `candidate_id` as the matching key
- accept raw bookmaker-paste entry blocks when event, market, side, and timing are sufficient for conservative matching
- promote matched rows into `Base_Entradas`
- update the candidate row instead of creating a new candidate

## Sport-specific structural rules
- Football: use league-aware logic. Distinguish between `strong-stat-coverage` and `weak-stat-coverage` environments.
- Football: use xG-centered reasoning only when the environment supports it.
- NBA: keep moneyline, spread, and game total as the launch core.
- NBA: player props must run through the restricted secondary module, not the core game-market workflow.
- NBA: supported prop markets in restricted scope are over/under `PTS`, `AST`, `REB`, `PA`, `PR`, `PRA`, and `3PM`.
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
