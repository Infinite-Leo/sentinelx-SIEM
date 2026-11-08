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