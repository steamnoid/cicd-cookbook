# Tradeoffs

## What this pattern makes harder

- “Quick” breaking API refactors require versioning or phased rollout.
- Teams must maintain a canonical contract artifact and keep it accurate.

## What it slows down

- Promotion speed if contract tooling is slow or contracts are large.
- Delivery of breaking changes (which should be slowed down by design).

## When NOT to use

- Truly private interfaces that never cross deployment boundaries (validate this assumption carefully).
- Systems where clients are deployed atomically with servers and can prove no skew (rare).

## Failure mode of overuse

If the contract diff rules are too strict or noisy, teams will normalize break-glass approvals. That produces friction without safety.
