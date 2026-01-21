# Automation

## What is enforced

Promotion requires a “telemetry contract” check.

Outcome is binary:
- Pass: release may be promoted.
- Fail: release is blocked until it emits required release-attributed telemetry.

## Where it lives

- In CI (build-time) as a required check: verify emitted fields exist in logs/trace instrumentation.
- In delivery (pre-promotion) as a runtime check: verify telemetry is visible and queryable in the target environment.

## How it works (implementation-neutral)

1) Define a minimal telemetry contract

Example contract items:
- log field: `release_id`
- trace attribute: `service.version` (or equivalent)
- metric strategy: one of:
  - separate canary/stable via routing label (preferred)
  - explicit cohort dimension with bounded values

2) Validate at build time
- Static checks for instrumentation presence (linting, compile-time assertions, log schema checks).

3) Validate at runtime
- Deploy canary at tiny percentage.
- Emit synthetic requests.
- Query backend to confirm telemetry is present and filterable by release/cohort.

4) Fail closed on missing attribution
- If the system can’t query “canary vs stable” reliably, do not promote.

## What happens when it blocks a change

- Teams add/standardize the release identity across log/trace contexts.
- Metric partitioning is adjusted to avoid high cardinality while still enabling cohort comparison.
