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

## Rule
If the request is vague, it must internally clarify the minimum necessary before proceeding.
