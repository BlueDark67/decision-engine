# core/input-standard.md

## Objective
This document defines the minimum inputs required by the system.

## Shared baseline fields
Any analysis should try to collect:

- event
- sport
- market
- side or selection
- current price
- price timestamp
- event time

## Daily batch envelope fields
When daily batch mode is active, the system should also collect:

- raw message
- received time
- batch id
- one raw candidate line per bullet
- inferred games date, when available

## Entry batch envelope fields
When entry batch mode is active, the system should try to collect for each entry block:

- candidate id
- odd_entrada
- hora_entrada
- observacoes, when provided

When the source is a raw bookmaker paste, the system should also try to collect:

- side from the first line of the block
- market from the market label line
- event from the matchup line
- kickoff from the event-time line
- ignore payout-only lines
- entry timestamp from the line after `Details`, when present

Fallback matching fields when candidate id is missing:

- event date
- event
- market
- side
- kickoff
- odd_entrada
- hora_entrada

## Baseline inputs by category
### Market
- exact market
- current price
- price timestamp

### Form and performance
- a recent window coherent with the sport
- opponent context, when relevant

### Availability and news
- injuries, absences, doubts, penalties, or equivalent updates
- information timestamp

### Schedule and context
- rest
- congestion
- travel
- competitive or strategic context

## Minimum inputs by sport
### Football
- teams
- competition
- kickoff
- market and price
- recent form
- availability or lineup expectation
- schedule context

### NBA
- teams
- tipoff
- market and price
- injury report with timestamp
- projected starters or rotation context
- rest and travel

### NBA Props (restricted secondary scope)
- player
- teams
- tipoff
- prop type
- side (`over` or `under`)
- line and price
- price timestamp
- injury report with timestamp
- projected role and minutes
- rotation context
- matchup context relevant to the prop family

### F1
- event
- timing mode
- market and price
- weather status
- penalties or news
- data available for the active mode

## Adequacy rule
Inputs must be adequate to the market being discussed. Examples:

- a total requires more than a generic read on which side is better
- an F1 H2H requires context specific to the phase of the weekend
- a football thesis based on xG requires sufficiently strong statistical coverage

## Input failure
If central inputs are missing for the selected market, the response should degrade to:

- `watchlist`, if the missing data could arrive before the event
- `insufficient data`, if the base is too weak
