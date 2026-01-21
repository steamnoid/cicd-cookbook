# Release-segmented telemetry

This pattern prevents “we can’t tell if the new version is the problem” failures by requiring production telemetry that can be segmented by release.

## Files

- [problem.md](problem.md)
- [failure_modes.md](failure_modes.md)
- [solution.md](solution.md)
- [automation.md](automation.md)
- [metrics.md](metrics.md)
- [tradeoffs.md](tradeoffs.md)

## What this pattern protects

During a rollout, you must be able to answer: “Is version N worse than N-1?” If you can’t segment telemetry by version, canary gating becomes blind and incident response slows down.

## Guardrail (binary)

A service cannot be promoted unless it emits a minimal telemetry set that is filterable by release identity (build id / image tag / git SHA) across logs, metrics, and traces (as applicable).
