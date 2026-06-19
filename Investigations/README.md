# 🕵️ Incident Investigations

This folder contains structured, analyst-style investigation write-ups for
attacks simulated in [Attacks/](../Attacks/README.md). Each investigation
follows a consistent format so it reads like a real SOC incident report.

## Investigation Template

```markdown
# Incident: <title>

## Summary
One or two sentences describing what happened.

## Timeline
| Time | Event |
|---|---|
| HH:MM | First indicator observed |
| HH:MM | Alert triggered |
| HH:MM | Investigation started |
| HH:MM | Containment/conclusion |

## Detection
Which alert fired, and the SPL query/log evidence.

## Analysis
Source IP, target, technique used, scope of impact (mapped to
MITRE ATT&CK where applicable).

## Root Cause
Why the activity was possible (misconfiguration, exposed service, etc.)

## Recommendation
What should change — firewall rule, detection tuning, patching, etc.

## Evidence
Relevant screenshots, raw log excerpts.
```

## Case Log

| # | Case | Related Attack | Status |
|---|---|---|---|
| — | — | — | No cases yet — investigations will be added as attacks are completed |
