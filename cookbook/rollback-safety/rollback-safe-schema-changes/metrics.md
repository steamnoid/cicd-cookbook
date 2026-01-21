# Metrics

These signals exist to verify the guardrail is catching real risk and to detect drift.

## Introduced signals

- Rollback-incompatible migration attempts (count)
- Rollback-incompatible migration attempts (rate per week)
- Time spent blocked by rollback gate (p50/p95)
- Number of break-glass overrides (count)

## Interpreting trends

Good trends:
- Attempts decrease over time as teams learn the sequencing.
- Blocked time decreases as migration templates and tooling mature.
- Overrides are rare and correlated with true emergencies.

Bad trends:
- Overrides become routine (guardrail is being bypassed instead of used).
- Attempts remain flat while schema churn increases (teams aren’t internalizing the invariant).
- Rollback incidents still happen after the gate exists (compat checks are not representative).

## Operational outcome metrics to watch

- Rollback success rate (rollbacks that restore health without additional code changes)
- Rollback MTTR (median time to restore service)
- Post-rollback database error rate (should stay near baseline)
