# Metrics

These signals verify the gate is preventing real risk and shaping behavior.

## Introduced signals

- Breaking contract diffs blocked (count)
- Breaking contract diffs blocked per service/interface (top offenders)
- Time-to-fix blocked contract diffs (p50/p95)
- Number of break-glass approvals (count)

## Interpreting trends

Good trends:
- Blocking events decrease as teams adopt additive/versioned change patterns.
- Break-glass is rare and correlated with true emergencies.

Bad trends:
- Break-glass is common (gate is being bypassed).
- Blocks concentrate in one service repeatedly (poor ownership or unclear contracts).
- Incident rate remains high despite blocks (contracts under-test or missing semantic coverage).

## Operational outcome metrics to watch

- Deploy-adjacent 4xx/5xx spikes caused by contract mismatch
- Downstream retry rates and queue depth during deploy windows
- Time-to-causality for client/server incompatibility incidents
