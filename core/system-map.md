# core/system-map.md

## Objective
This document defines the structural map of the system.

## Balanced architecture
The system follows a balanced model:

- a shared core for intake, quality, risk, gate, and output
- sport-specific modules for football, NBA, and F1

## Shared core
### 1. Intake
Normalizes the request:

- event
- market
- side
- price
- time
- analysis objective

### 2. Input Audit
Checks:

- whether minimum inputs exist
- whether the inputs are fresh
- whether the context covers the market being discussed

### 3. Data Quality Assessment
Evaluates the robustness of the data.

### 4. Sport Analysis
Produces the sport-specific read.

### 5. Market Evaluation
Translates the read into market logic.

### 6. Edge Quality Assessment
Evaluates whether the advantage is clear, marginal, or absent.

### 7. Risk Load Assessment
Measures fragility, volatility, and uncertainty.

### 8. Red Flag Audit
Looks for factors capable of weakening or vetoing the thesis.

### 9. Decision Gate
Converts the analysis into:

- `enter`
- `pass`
- `watchlist`
- `insufficient data`

### 10. Output Composer
Forces the final response into the project schema.

## Modules by sport
### Football
- league-aware reading
- statistical coverage mode
- tactical and statistical interpretation
- translation into core markets

### NBA
- availability and rotation
- rest, travel, and schedule
- matchup and style
- translation into core markets

### F1
- structural timing mode
- one-lap pace versus race pace
- strategy and reliability
- translation into core markets

## Structural rule
No specific module may skip the core. The sport adds its own layer, but does not replace:

- data quality
- edge quality
- risk load
- red flags
- the gate
