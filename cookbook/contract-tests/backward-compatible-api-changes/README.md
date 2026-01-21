# Backward-compatible API changes

This pattern prevents breaking API changes from reaching production by enforcing a contract gate against the last promoted interface.

## Files

- [problem.md](problem.md)
- [failure_modes.md](failure_modes.md)
- [solution.md](solution.md)
- [automation.md](automation.md)
- [metrics.md](metrics.md)
- [tradeoffs.md](tradeoffs.md)

## What this pattern protects

In distributed systems, API changes propagate through multiple independent deployment timelines. A producer must not ship an API contract that breaks existing callers.

## Guardrail (binary)

If an API contract diff versus the last promoted contract contains a breaking change, promotion is blocked unless the change is explicitly versioned.
