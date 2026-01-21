# Automation

## What is enforced

Promotion between rollout stages is gated by SLO/SLI evaluation on the canary population.

Outcome is binary:
- Pass: promotion may proceed.
- Fail: promotion is blocked and rollout halts (or automatically rolls back, if configured).

## Where it lives

- In the delivery pipeline between rollout stages (e.g., 1% → 5% → 25% → 100%).
- Optionally mirrored as an admission guard (prevent further scheduling of the new version while breached).

## How it works (implementation-neutral)

1) Identify canary traffic
- Metrics must be filterable by the deployed version (image tag/build id) or by canary routing label.

2) Evaluate a small SLO gate set
- Select 1–3 SLIs that represent user impact.
- Evaluate them over a canary window with explicit minimum volume and duration.

3) Compare against a baseline
- Prefer an in-parallel control group (stable pool) to remove global traffic shifts.
- If using historical baseline, keep the window tight and protect against diurnal changes.

4) Decide pass/fail
- Fail if SLO is breached.
- Fail if regression exceeds threshold (e.g., error rate delta, latency ratio).
- Fail closed when metrics are missing or unqueryable.

5) On failure
- Freeze promotion.
- Emit a machine-readable reason (which SLI failed, canary vs baseline, window, volume).
- Optionally trigger automated rollback when the canary fraction is still small.

## What happens when it blocks a change

- The rollout stops before broad exposure.
- The change is fixed (performance, dependency behavior, configuration) or shipped behind a safer rollout plan.
- If the regression is acceptable, thresholds are adjusted explicitly; do not bypass silently.
