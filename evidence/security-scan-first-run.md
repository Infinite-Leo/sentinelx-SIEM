# Security Scan First Run

Date: 8 November 2026
Workflow: Security scans
Commit: e917b0d

## Bandit
Findings: 1
Highest severity: LOW
Finding: `backend/app/scenarios/runner.py:114` — standard pseudo-random generator reported by Bandit B311.

## npm audit
Findings: Not available from this run.
Highest severity: Not available.
Result: `npm audit` returned `ENOLOCK` because the frontend has no npm lockfile. This is a scan limitation, not a clean result.

## Trivy
Findings: 74
Highest severity: CRITICAL
Breakdown: 1 CRITICAL, 32 HIGH, 34 MEDIUM, 7 LOW.
Notable result: PyJWT 2.11.0 was reported with a CRITICAL authentication-bypass issue; Trivy listed 2.14.0 as the fixed version.

## Remediation
Finding selected: Bandit B311 in `backend/app/scenarios/runner.py`.
Change made: Replaced the standard `random.uniform()` call used for scenario jitter with `secrets.SystemRandom().uniform()`.
Reason: The simulation still receives non-deterministic jitter, while the code no longer uses the PRNG that Bandit flags for security-sensitive randomness.
Retest result: Pending the next GitHub Actions run. The original finding remains preserved in this first-run record.
