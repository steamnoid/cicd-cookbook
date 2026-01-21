# Rollback-safe schema changes

This pattern prevents “rollback turns into incident” failures caused by database schema changes that make the previous service version unable to run.

## Files

- [problem.md](problem.md)
- [failure_modes.md](failure_modes.md)
- [solution.md](solution.md)
- [automation.md](automation.md)
- [metrics.md](metrics.md)
- [tradeoffs.md](tradeoffs.md)

## What this pattern protects

Rollback must remain a low-risk operation. A deploy that permanently removes the ability to roll back (because the database changed shape) converts routine recovery into a high-risk incident.

## Guardrail (binary)

Changes that include schema migrations must prove that the immediately previous production version (N-1) can still run correctly against the migrated schema.
