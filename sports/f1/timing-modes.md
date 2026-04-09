# sports/f1/timing-modes.md

## Objective
Define F1 timing modes and required evidence by weekend phase, including sprint-weekend treatment.

Circuit weighting reference: see `sports/f1/circuit-registry.md`.
Sprint variant reference: see `sports/f1/sprint-weekend.md`.

## Pre-Practice
### Core inputs
- track type
- baseline form
- weather outlook
- penalties or news

### Rule
Conservative mode by default.

## Post-Practice
### Core inputs
- practice pace
- long-run pace
- degradation signals
- initial readiness

### Rule
Allows stronger reads, but still conditional.

## Post-Qualifying
### Core inputs
- grid
- confirmed one-lap pace
- updated penalties
- track-position context

### Rule
Often the cleanest mode for several H2H and placement markets.

## Pre-Race
### Core inputs
- final weather
- final penalties
- strategic context
- reliability and starting conditions

### Rule
Final gate before entry.

## Sprint-weekend note
When sprint format is active, apply the dedicated variant in `sports/f1/sprint-weekend.md`, including `usable` data-quality ceilings for Sprint Qualifying and Sprint Race modes.

## Technical factors
### Tyre degradation
- High-deg circuits can neutralize one-lap pace advantages over race distance.
- In H2H race markets, increase the weight of long-run degradation behavior versus raw qualifying pace.

### DRS zones
- Circuits with multiple effective DRS zones reduce pure grid-advantage persistence in race conditions.
- At these tracks, qualifying edge should be discounted relative to race-pace and overtaking capacity.

### Temperature sensitivity
- Some teams are disproportionately affected by ambient temperature (especially cooling-limited packages).
- Flag temperature sensitivity as a contextual factor that can override baseline pace assumptions.

## Circuit-profile weighting rule
Use `sports/f1/circuit-registry.md` to weight qualifying versus race-pace evidence:
- high-downforce or street tracks: raise qualifying and track-position weight
- low-downforce power tracks: raise race-pace, DRS, and overtaking weight
- high-deg tracks: raise tyre-management and strategy weight
