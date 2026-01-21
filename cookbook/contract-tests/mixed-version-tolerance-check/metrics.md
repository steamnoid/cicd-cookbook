# Metrics

These signals verify that mixed-version risk is being detected before production.

## Introduced signals

- Mixed-version contract failures (count)
- Mixed-version contract failures by interface/direction (top offenders)
- Time blocked by mixed-version gate (p50/p95)
- Number of “contract changes without version bump” caught (count)

## Interpreting trends

Good trends:
- Failures trend down as contracts stabilize.
- Failures concentrate in a few interfaces, then disappear after redesign/versioning.

Bad trends:
- Failures remain flat while deploy frequency increases (risk is accumulating).
- Directional failures repeat (e.g., N→N-1 breaks repeatedly), indicating a consistent rollout-order assumption.
- Teams add frequent overrides (guardrail is being bypassed).

## Operational outcome metrics to watch

- Rollout-time error rate delta (deploy windows vs baseline)
- DLQ depth and retry rate during deploy windows
- Canary false-positive rate (rollbacks triggered by mixed-version artifacts)
