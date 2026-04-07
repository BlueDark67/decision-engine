# CONTEXTO.md

## Objective
This project exists to structure analysis and decision-making in sports betting, with initial focus on:

- football
- NBA
- Formula 1

It is not an automated prediction system. It is a disciplined thinking system.

## Practical purpose
The project should help:

- organize reasoning before entering a bet
- improve consistency across analyses
- reduce impulsiveness
- separate data, interpretation, and decision
- make it visible when a bet should be avoided

## Launch scope
### Football
- 1X2
- DNB
- Asian Handicap
- totals
- BTTS

### NBA
- moneyline
- spread
- game total

## Restricted secondary scope
### NBA player props
- over/under points (`PTS`)
- over/under assists (`AST`)
- over/under rebounds (`REB`)
- over/under points + assists (`PA`)
- over/under points + rebounds (`PR`)
- over/under points + rebounds + assists (`PRA`)
- over/under made threes (`3PM`)

### F1
- qualifying H2H
- race H2H
- top 6
- top 10
- winner and podium only selectively

## Outside the launch core
- automations
- APIs
- automated live fetching
- proprietary projection models

## Operational tracking layer
- a fixed Google Sheets tracker may be used as an operational layer
- this tracker stores daily candidates, active watchlist items, and final entries
- it does not replace the core analysis or turn the system into automated live fetching
- it must reuse the same file instead of creating daily spreadsheets
- final entries may also be reported in batch through a dedicated entry-promotion trigger

## Inputs the system should be able to accommodate
Even without automated implementation, the system should be ready to work with:

- odds
- recent form
- injuries or news
- schedule and competitive context

## Guiding question
Every analysis should converge on a disciplined answer to this question:

> Should I enter, pass, watch, or assume there is not enough data?

## Project philosophy
- a well-justified `pass` is better than a forced `enter`
- a disciplined `watchlist` is better than a rushed conclusion
- it is better to recognize limits than to hide uncertainty behind confident language

## Modes by sport
### Football
The system must be league-aware and adapt its reasoning type to the real quality of statistical coverage.

### NBA
The system must prioritize rotation context, availability, rest, travel, and matchup.

### F1
The system must change structurally with the phase of the weekend:

- pre-practice
- post-practice
- post-qualifying
- pre-race
