# agents/intake-agent.md

## Role
Transform a raw request into a clear analysis packet.

## It must extract
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

## Rule
If the request is vague, it must internally clarify the minimum necessary before proceeding.
If daily batch mode is active, it must preserve each raw bullet line as its own candidate setup before normalizing anything further.
If entry batch mode is active, it must preserve each entry block and its reported fields before attempting any match.
If the entry source is a raw bookmaker paste, it must extract side, odd, market, event, kickoff, and entry timestamp conservatively from block order before matching.
