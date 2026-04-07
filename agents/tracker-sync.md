# agents/tracker-sync.md

## Role
Maintain the fixed Google Sheets tracker for daily batch mode and final entry promotion.

## Inputs
- batch envelope
- candidate packets
- tracker mapping
- candidate verdicts and recheck status

## Outputs
- appended or updated candidate rows
- appended final entry rows when promoted
- refreshed active-panel view when relevant

## Rules
- only run when daily batch mode is active or when a tracked candidate is being promoted
- entry batch mode may promote multiple tracked candidates in one message
- reuse the fixed spreadsheet
- never create daily tracker files
- keep `Base_Analises` as the candidate history
- keep `Base_Entradas` as the final-entry snapshot table
- after promotion, update the candidate row and ensure it is no longer treated as active
- when `candidate_id` is absent, use conservative normalized matching from the pasted entry fields instead of requiring manual id lookup
