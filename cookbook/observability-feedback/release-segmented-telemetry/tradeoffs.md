# Tradeoffs

## What this pattern makes harder

- Teams must standardize logging/tracing fields across codebases.
- Some observability systems require careful configuration to avoid high-cardinality labels.

## What it slows down

- Promotion, because runtime verification requires a small deploy + query step.
- Delivery when observability backends are unstable (gate fails closed).

## When NOT to use

- Services that do not participate in progressive delivery and cannot be compared during rollout.
- Systems with no meaningful production telemetry path (in which case SLO gating also cannot work).

## Failure mode of overuse

If enforced without a bounded identity strategy, teams may add unbounded labels, causing telemetry loss or cost blowups.
