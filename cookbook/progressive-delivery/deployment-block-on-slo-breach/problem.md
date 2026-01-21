# Problem

Progressive delivery expands blast radius unless promotion is gated on user-impact signals.

A canary rollout often sees the first real evidence of a regression: dependency behavior, data distributions, cache warmup effects, and production traffic shape. If promotion continues based on time delays or human review alone, the system can promote a version that is already violating the service’s SLO.

## How it manifests

- Canary shows elevated error rate or latency, but rollout continues.
- Operators notice only after the rollout reaches a large percentage.
- Teams roll back late, after queues/backlogs and downstream impacts have accumulated.

## Why naive CI/CD pipelines miss it

- CI validates correctness in controlled environments, not real production load and dependencies.
- “Wait N minutes” canary steps detect only crashes, not user-impact regressions.
- Human review is inconsistent and slow relative to rollout automation.
