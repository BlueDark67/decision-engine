# agents/INDEX.md

## Objective
This directory defines the conceptual agents of the system.

## Participation order
1. `system-orchestrator`
2. `intake-agent`
3. `evidence-auditor`
4. sport-specific agent
5. `market-analyst`
6. `risk-controller`
7. `decision-gatekeeper`
8. `tracker-sync`, when daily batch mode is active
9. `output-composer`

In entry batch mode, the flow is:
1. `system-orchestrator`
2. `intake-agent`
3. `tracker-sync`
4. `output-composer`

## Rule
The agents are responsibility modules, not free-form personalities. Each one must return output that is usable by the next module.
