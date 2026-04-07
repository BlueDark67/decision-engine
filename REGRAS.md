# REGRAS.md

## Purpose of this file
This document defines the system's analytical discipline rules.

## Core rules
- Separate data from interpretation.
- Separate interpretation from decision.
- Make the main drivers of the read explicit.
- Recognize uncertainty when inputs are incomplete.
- Avoid confident language without proportional support.

## Daily batch trigger rules
- Only activate daily batch mode when the trimmed raw message starts with `Análises do dia:` and ends with `Abraço`.
- If either boundary is missing, do not write to the Google Sheets tracker.
- In daily batch mode, each bullet is a candidate for evaluation, not a final bet.
- Reuse the fixed tracker file and never create a new daily spreadsheet.
- A quick batch verdict must still keep `data quality`, `edge quality`, and `risk load` separate.
- Promotion from candidate to final entry requires later recheck and current-price compatibility.

## Entry batch trigger rules
- Only activate entry batch mode when the trimmed raw message starts with `Entradas feitas:`.
- No closing phrase is required for entry batch mode.
- Prefer `candidate_id` to match each promoted entry to an existing candidate.
- Also accept raw bookmaker-paste entry blocks when they contain enough identifying information.
- Do not create a new candidate row when the intent is entry promotion.
- If matching is ambiguous, do not promote silently.
- Normalize common market labels and side labels conservatively before fallback matching.
- Promotion must write a final snapshot to `Base_Entradas`, update the linked `Base_Analises` row, and remove the item from the active operational view on the next sync.

## Mandatory core rules
- Never treat `data quality`, `edge quality`, and `risk load` as the same thing.
- Never issue `enter` without passing through the decision gate.
- Never omit relevant red flags.
- Never ignore timing when the market depends on it.
- Never use a narrative thesis as a substitute for sufficient evidence.

## Football-specific rules
- Always classify the environment as `strong-stat-coverage` or `weak-stat-coverage`.
- Only use xG-centered reasoning when both coverage and sample size allow it.
- When coverage is weak, use conservative mode.

## NBA-specific rules
- Keep moneyline, spread, and game total as the NBA launch core.
- Handle player props only through the dedicated restricted-scope props workflow.
- Supported prop markets in restricted scope are over/under `PTS`, `AST`, `REB`, `PA`, `PR`, `PRA`, and `3PM`.
- Prioritize availability, rotation, rest, and travel spots.
- Do not finalize strong reads based on injury news without a timestamp.
- Do not promote NBA props when minutes are unstable, role is unclear, or injury context is not confirmed.

## F1-specific rules
- Treat each timing mode as a different structure.
- Do not reuse the same level of confidence between `pre-practice` and `pre-race`.
- Do not overstate conviction on weekends where the data is still incomplete.

## Gate rules
- `enter` requires sufficient data, clear edge, and controlled risk load.
- `pass` should be used when the read exists but does not justify the risk or the price.
- `watchlist` requires an explicit trigger.
- `insufficient data` should be used when the inputs do not support responsible analysis.

## Exclusion rules
Avoid responses with these characteristics:

- vague
- impressionistic
- internally contradictory
- too narrative-driven
- too aggressive in conclusion relative to weak data

## Methodological honesty rule
Whenever the thesis is limited in strength, that must appear both in the body of the analysis and in the final stability or confidence note.
