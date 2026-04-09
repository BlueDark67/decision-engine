# core/quality-matrix.md

## Objective
Define hard cross-constraints between `data_quality`, `edge_quality`, and `risk_load` so the decision gate cannot overstate confidence.

## Constraint table
| Condition | Forced constraint | Gate impact |
| --- | --- | --- |
| `data_quality = weak` | `edge_quality` maximum becomes `marginal` (auto-downgrade if higher) | Prevents `clear` edge claims under weak data foundations |
| `data_quality = insufficient` | `edge_quality` forced to `none` regardless of factors | Strongly favors `insufficient data` or `pass` |
| `risk_load = extreme` | `decision_gate` cannot emit `enter` regardless of edge | Allowed outcomes: `pass`, `watchlist`, or `insufficient data` |
| `edge_quality = none` | `decision_gate` forced to `pass` or `insufficient data` | `enter` and `watchlist` are blocked unless edge changes after re-analysis |

## Enforcement order
1. Rate `data_quality` first.
2. Rate sport read and market evaluation.
3. Rate provisional `edge_quality`.
4. Apply matrix constraints to edge.
5. Rate `risk_load`.
6. Apply gate-level constraints from `risk_load` and final edge.
7. Emit final decision output.

## Derived max-allowed grid
| Data Quality | Max allowed Edge Quality |
| --- | --- |
| `strong` | `clear` |
| `usable` | `clear` |
| `weak` | `marginal` |
| `insufficient` | `none` |

## Gate restriction grid
| Edge Quality | Risk Load | Allowed gate outputs |
| --- | --- | --- |
| `none` | any | `pass`, `insufficient data` |
| `unclear` | `low`, `medium`, `high` | `pass`, `watchlist` |
| `marginal` | `low`, `medium` | `watchlist`, `pass` |
| `marginal` | `high` | `pass`, `watchlist` |
| `clear` | `low`, `medium`, `high` | `enter`, `watchlist`, `pass` |
| `clear` | `extreme` | `pass`, `watchlist`, `insufficient data` |
| any | `extreme` | `enter` is blocked |
