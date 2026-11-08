# Custom Correlation Rule

## Local Brute Force Login Detector

This custom threshold rule detects repeated failed authentication events from the same source.

| Field | Value |
| --- | --- |
| Rule type | Threshold |
| Severity | High |
| Event filter | `source_type=auth`, `event_type=login_failure` |
| Threshold | 5 events |
| Window | 300 seconds |
| Grouping | `source_ip` |

## Test result

The rule was tested against the local SentinelX event history.

- Events evaluated: 29
- Alerts that would fire: 1
- Test type: Historical dry-run
- Live simulation result: 29 events ingested and 0 live alerts generated

The dry-run result demonstrates that the rule matches the simulated brute-force pattern. It does not claim that a live alert was generated during the original simulation.

## Live validation

After the rule was enabled, the Brute Force with Lateral Movement playbook was run again locally. The run ingested 29 events and generated 2 High-severity alerts for source group `203.0.113.42`, each matching 5 `login_failure` events. Both alerts were acknowledged, investigated, and resolved by the local analyst account. The dashboard showed 2 total alerts, 0 open alerts, and 0 critical alerts after resolution.
