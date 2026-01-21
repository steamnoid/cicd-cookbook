# Mixed-version tolerance check

This pattern prevents rollout-time outages caused by mixed-version fleets (N and N-1 running simultaneously) that are unable to interoperate.

## Files

- [problem.md](problem.md)
- [failure_modes.md](failure_modes.md)
- [solution.md](solution.md)
- [automation.md](automation.md)
- [metrics.md](metrics.md)
- [tradeoffs.md](tradeoffs.md)

## What this pattern protects

A rolling deploy must be safe while versions are mixed. The system must tolerate:

- new producers interacting with old consumers
- old producers interacting with new consumers
- old clients calling new servers and new clients calling old servers (as applicable)

## Guardrail (binary)

A change cannot be promoted unless it passes a mixed-version contract suite that proves N and N-1 can interoperate on the defined interfaces.
