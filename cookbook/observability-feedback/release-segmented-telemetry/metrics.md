# Metrics

These signals show whether release segmentation is present and useful.

## Introduced signals

- Telemetry contract failures (count)
- Promotions blocked due to missing segmentation (count)
- Time-to-causality during incidents (deploy suspected → confirmed/refuted)
- Percentage of requests with release-attributed traces/logs (coverage)

## Interpreting trends

Good trends:
- Contract failures decrease as instrumentation becomes standardized.
- Coverage approaches 100% for critical paths.
- Time-to-causality shrinks for deploy-adjacent incidents.

Bad trends:
- Teams bypass the gate (overrides) rather than fixing instrumentation.
- Coverage remains low on high-impact endpoints.
- Metric cardinality/cost spikes (segmentation implemented unsafely).

## Operational outcome metrics to watch

- Canary gate accuracy (fewer false positives/negatives due to better segmentation)
- Rollout-induced incident rate
- Mean time to rollback decision for deploy-adjacent regressions
