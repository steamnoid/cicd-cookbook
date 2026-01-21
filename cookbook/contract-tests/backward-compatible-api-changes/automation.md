# Automation

## What is enforced

A contract-diff gate runs before merge and/or before promotion.

Outcome is binary:
- Pass: no breaking changes detected relative to the last promoted contract.
- Fail: breaking change detected; change is blocked unless versioned.

## Where it lives

- Pre-merge CI: fast feedback for developers.
- Pre-promotion delivery: protects manual hotfix and alternative merge paths.

## How it works (implementation-neutral)

1) Define the canonical contract artifact

Examples:
- HTTP: OpenAPI/JSON schema contract
- RPC: IDL/proto contract

The key is that the artifact is machine-diffable and reflects what production exposes.

2) Fetch the baseline

Baseline should be the last promoted contract (not “main branch”). Typical sources:
- artifact registry
- last release tag
- last promoted build metadata

3) Compute a compatibility diff

- Parse both contracts.
- Identify breaking deltas (removals, renames, required fields, type changes, validation tightening).
- For semantic changes, require an explicit marker (version bump or explicit compatibility claim).

4) Fail with a precise reason

The failure output must name:
- interface and endpoint/method
- direction: callers N-1 → server N
- the breaking delta

5) Provide an escape hatch with friction

If a breaking change is unavoidable:
- require explicit versioning
- or require a “break-glass” approval path with recorded justification

The default path must be safe; exceptions must be rare and visible.
