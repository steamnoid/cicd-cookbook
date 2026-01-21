# Metrics

These signals confirm the gate is catching real risk and not generating noise.

## Introduced signals

- Promotion blocks due to SLO breach (count)
- Promotion blocks by SLI (top triggers)
- Promotion blocks by service/team (hot spots)
- Gate evaluation missing-data failures (count)
- Gate time overhead per deploy (p50/p95)

## Interpreting trends

Good trends:
- Blocks correlate with real regressions found early.
- Missing-data failures trend toward zero (observability completeness improves).
- Gate overhead is stable and predictable.

Bad trends:
- Frequent blocks with no corresponding production symptoms (false positives).
- Frequent missing-data failures (gate is failing closed because telemetry is unreliable).
- Overrides become routine (gate is being bypassed rather than tuned).

## Operational outcome metrics to watch

- Error budget burn rate during deploy windows
- Rollout-induced incident rate
- Mean time from regression start → promotion halted
