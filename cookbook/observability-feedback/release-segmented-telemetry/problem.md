# Problem

Rollouts and incidents become guesswork when telemetry cannot be segmented by release.

Many teams have “global” telemetry: aggregated latency and error rate, logs without consistent version fields, traces without release attributes. During deployment, this prevents isolating whether the candidate release (N) is causing a regression versus a broader dependency or traffic shift.

## How it manifests

- Canary is 1–5%, but global metrics look unchanged, so promotion proceeds.
- Incident response cannot answer “is it only the new version?” quickly.
- Teams roll back based on intuition, or delay rollback because evidence is unclear.

## Why naive CI/CD pipelines miss it

- CI validates code, not observability completeness.
- Progressive delivery assumes the system can compare canary vs baseline; without segmentation, you cannot.
- Missing release attribution is rarely a test failure; it fails only under pressure.
