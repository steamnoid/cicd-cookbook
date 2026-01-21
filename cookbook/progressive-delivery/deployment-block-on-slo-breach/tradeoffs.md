# Tradeoffs

## What this pattern makes harder

- Teams must maintain reliable, version-filterable production telemetry.
- SLO definitions and ownership must be explicit; otherwise the gate becomes arbitrary.

## What it slows down

- Promotion speed due to mandatory evaluation windows.
- Delivery when traffic is too low to reach minimum-volume thresholds.

## When NOT to use

- Services without meaningful production SLIs (no traffic, no user impact); gate will be random.
- Systems where rollback/abort is not possible and the delivery mechanism cannot halt safely.

## Failure mode of overuse

If gates are too sensitive or too broad, teams will normalize overrides and the stop condition will stop working in practice.
