# Solution

## Invariant

For any service under progressive delivery, production telemetry must support a version-to-version comparison during rollout.

At minimum:

- logs: include a stable release identity field
- traces: include release identity as a resource/span attribute
- metrics: allow separating canary vs baseline without unbounded cardinality

## Why this invariant matters under continuous change

A rollout is an experiment. Without segmentation, you cannot measure the experiment’s effect, so promotion decisions become time-based or manual.

This invariant enables:

- canary gating based on SLO/SLI deltas
- fast rollback confidence (causality)
- faster RCA by reducing hypothesis space

## Define “release identity” precisely

Use a bounded identifier that is consistent across telemetry types:

- build id, image tag, or git SHA

Also include a coarse “rollout cohort” field when useful:

- stable vs canary (or stage)

The goal is filtering and comparison, not perfect provenance.
