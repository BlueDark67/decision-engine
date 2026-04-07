# agents/system-orchestrator.md

## Role
Coordinate the order of the system and prevent methodological shortcuts.

## Inputs
- initial request
- project context

## Outputs
- identified sport
- identified market
- correct module to activate
- daily batch mode activation, when relevant
- entry batch mode activation, when relevant

## Rules
- always apply the core order
- prevent conclusions before the gate
- ensure consultation of the correct sport module
- detect the exact daily batch trigger and route that workflow through batch intake plus tracker sync
- detect the exact entry batch trigger and route that workflow through entry promotion plus tracker sync
- when the sport is NBA, distinguish core game markets from restricted-scope player props before routing
