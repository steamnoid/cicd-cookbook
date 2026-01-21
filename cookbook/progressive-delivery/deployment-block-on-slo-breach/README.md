# Deployment block on SLO breach

This pattern prevents progressive rollouts from expanding blast radius when production user-impact signals degrade during canary.

## Files

- [problem.md](problem.md)
- [failure_modes.md](failure_modes.md)
- [solution.md](solution.md)
- [automation.md](automation.md)
- [metrics.md](metrics.md)
- [tradeoffs.md](tradeoffs.md)

## What this pattern protects

Canary is only a safety mechanism if it can stop promotion based on production signals. This pattern protects the invariant that a rollout cannot proceed while it is actively harming the SLO.

## Guardrail (binary)

Promotion is blocked if the canary window shows an SLO breach or an agreed regression beyond tolerance.
