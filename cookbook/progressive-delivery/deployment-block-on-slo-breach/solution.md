# Solution

## Invariant

A rollout may not progress while the canary is breaching the SLO or burning the error budget above an agreed threshold.

This is a production safety invariant: promotion depends on user-impact signals, not elapsed time.

## Why this invariant matters under continuous change

As deploy frequency increases, human review does not scale. The system needs an automatic stop condition that triggers before broad user impact.

## Define “breach” precisely

Choose a small set of SLIs that represent real user impact for the service (examples: request success rate, p95 latency, saturation of a critical dependency).

Define breach/regression in a way the pipeline can evaluate:

- Absolute breach: SLI violates the SLO during the canary window.
- Regression breach: canary SLI is worse than baseline by more than an allowed delta.

Baseline must be explicit:
- concurrent control group (stable version / non-canary pool), or
- recent historical window immediately before canary starts

Also define minimum data requirements:
- minimum request volume
- minimum evaluation duration

Without minimums, the gate becomes random and gets bypassed.
