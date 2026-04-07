# core/entry-batch-mode.md

## Objective
Define the disciplined operating mode for promoting multiple confirmed entries into the fixed tracker in one message.

## Activation trigger
This mode activates only when the raw user message, after trimming outer whitespace, starts with the exact string `Entradas feitas:`.

No closing phrase is required.

If this starting trigger is missing, entry batch mode must not activate.

## Central interpretation rule
In this mode, the message is not asking for a fresh candidate analysis batch. It is reporting that one or more entries were actually taken.

The purpose is to:

- locate the existing candidate rows
- promote them into `Base_Entradas`
- snapshot the final entry details
- mark the corresponding candidate rows as `entrada_confirmada`
- remove them from the operational active view on the next sync

## Preferred matching rule
The preferred key is `candidate_id`.

Each reported entry should include:

- `candidate_id`
- `odd_entrada`
- `hora_entrada`

Optional:

- `observacoes`

## Supported input styles
Entry batch mode must support both of these styles:

### Structured promotion style
- one block per entry
- explicit `campo: valor` lines
- preferred when available

### Raw bookmaker-paste style
- copied directly from the bookmaker slip or bet history
- no `candidate_id`
- no explicit field labels
- one block per entry, typically containing selection, odd, market, event, kickoff, and an entry timestamp near `Details`
- for player props, the block may also expose player identity, prop line, prop side, or book wording variants that must be normalized instead of discarded

The system should not require the user to manually fetch tracker ids when the bookmaker paste already contains enough identifying information.

## Fallback matching rule
If `candidate_id` is missing, the system must attempt a strict fallback match using the best available combination of:

- `data_jogo`
- `evento`
- `mercado`
- `lado`
- `odd_entrada`
- `hora_entrada`

If the fallback match is ambiguous, do not promote the entry silently. Keep the ambiguity explicit.

If the row is a player prop, fallback matching should instead prefer:

- `data_jogo`
- `evento`
- `prop_player`
- `prop_type`
- `prop_line`
- `prop_side`
- `hora_entrada`

## Parsing rule
Inside the entry batch envelope:

- the first non-empty line must be `Entradas feitas:`
- each following non-empty line beginning with `-` starts a new structured entry block
- in structured style, the text immediately after `-` may serve as a human label, but it does not replace structured fields
- in structured style, subsequent non-empty lines in the block should be parsed as `campo: valor`
- in raw bookmaker-paste style, blank lines and the sequence around `Possible payout` / `Details` may delimit one entry from the next
- blank spacer lines should be ignored

## Raw bookmaker-paste interpretation rule
When the message is a bookmaker paste, the system should read the entry block conservatively as:

1. selection or side
2. odd_entrada
3. market
4. event
5. kickoff
6. optional payout line to ignore
7. optional `Details` marker
8. entry timestamp

If one of these fields is missing or displaced, keep the uncertainty explicit instead of forcing a match.

When the bookmaker paste is a player prop, the system should also try to isolate:

1. player name
2. prop type
3. prop line
4. over or under side
5. event
6. kickoff
7. optional book wording or timestamp details

## Example structured style
```text
Entradas feitas:

- Sporting over 0.5
candidate_id: CAND-20260407-001
odd_entrada: 1.47
hora_entrada: 2026-04-07 18:10
observacoes: linha mantida dentro da faixa

- Bayern dnb
candidate_id: CAND-20260407-002
odd_entrada: 1.71
hora_entrada: 2026-04-07 19:02
```

## Example bookmaker-paste style
```text
Entradas feitas:

Bayern Munich
1.74
Draw no bet
Real Madrid vs Bayern Munich
07/04, 20:00
Possible payout: EUR 0.87

Details
07/04, 08:25

yes
1.63
Both teams to score
Wrexham AFC vs Southampton FC
07/04, 20:00

Possible payout: EUR 0.81

Details
07/04, 08:26
```

## Required processing order
1. Detect the entry batch trigger.
2. Detect whether the body is structured style or raw bookmaker-paste style.
3. Split the message into entry blocks.
4. Normalize each block into entry fields.
5. Match each block to an existing candidate row.
6. Validate that the candidate is still eligible for promotion.
7. Append one final snapshot row to `Base_Entradas` per confirmed entry.
8. Update the matching `Base_Analises` rows with `entry_id`, `flow_status`, and `updated_at`.
9. Refresh `Painel_Ativo` so promoted rows are no longer shown as active.

## Normalization rule
Before fallback matching, the system should normalize:

- market labels such as `Draw no bet` -> `DNB`
- common side labels such as `yes` -> `Yes`
- event names and team naming variants where the matchup is clearly the same
- day/month timestamps into the active year when the surrounding context supports it
- prop labels such as `Points` -> `PTS`, `Assists` -> `AST`, `Rebounds` -> `REB`, `Points + Assists` -> `PA`, `Points + Rebounds` -> `PR`, `Points + Rebounds + Assists` -> `PRA`, `Made Threes` / `3-pointers made` -> `3PM`
- prop sides such as `Over`, `Under`, `Mais de`, or `Menos de` into the controlled tracker labels
- player naming variants where the identity is clearly the same

## Eligibility rule
Do not promote a candidate if:

- the match to the candidate row is ambiguous
- the candidate was already promoted
- the candidate was closed or discarded in a conflicting way
- the reported entry details are incomplete for snapshot purposes
- the bookmaker-paste block cannot be normalized with enough confidence

## Snapshot rule
The row written to `Base_Entradas` must preserve the approval-time snapshot:

- final odd
- final timestamp
- final observations
- final verdict context

Later changes to the candidate row must not silently rewrite this snapshot.

## Output policy
When this mode is active, a compact promotion summary is acceptable in chat. The main operational requirement is accurate tracker sync, not a full fresh analysis output per entry.
