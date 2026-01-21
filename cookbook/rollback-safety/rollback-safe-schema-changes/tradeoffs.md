# Tradeoffs

## What this pattern makes harder

- Single-shot “do everything in one migration” changes become slower because they must be phased.
- Teams must maintain temporary compatibility code paths (dual reads/writes, fallbacks).

## What it slows down

- Delivery of schema-breaking refactors, because the contract (destructive) step is delayed.
- CI time and infrastructure use, because N-1 checks require provisioning and execution.

## When NOT to use

- Systems where rollback is not an accepted recovery strategy (e.g., immutable forward-only migrations with a different, proven recovery mechanism).
- Datastores where schema is not centrally controlled or is effectively schemaless and compatibility is enforced entirely in application-level contracts.

## Failure mode of overuse

If the gate is too strict or unrepresentative, teams will normalize overrides. That produces the worst outcome: extra friction without real safety.
