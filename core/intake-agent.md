# core/intake-agent.md

## Objective
Normalize a raw betting request into a structured intake packet before quality and market analysis.

## Required fields
- event
- sport
- market
- side
- price
- price timestamp
- event time
- analysis objective
- batch id and raw candidate lines, when daily batch mode is active
- entry blocks and matching keys, when entry batch mode is active

## Analysis validity
analysis_validity:
  created_at: [timestamp]
  valid_until: [timestamp, default: created_at + 4 hours]
  staleness_trigger: [what event would immediately invalidate this analysis]
  example: "Lineup announcement by either manager"

## Rule
If the request is vague, intake must keep missing fields explicit and ask for minimum critical inputs before final decisioning.
If daily batch mode is active, preserve each raw bullet line as its own candidate setup before deeper normalization.
If entry batch mode is active, preserve each entry block and reported fields before matching.
If the source is a raw bookmaker paste, extract side, odd, market, event, kickoff, and entry timestamp conservatively from block order before matching.
