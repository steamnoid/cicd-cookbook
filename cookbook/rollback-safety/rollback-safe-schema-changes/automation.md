# Automation

## What is enforced

Any change set that includes a schema migration must pass a rollback-compatibility gate:

- After migration, the previous production version (N-1) must still pass a defined compatibility check suite.

Outcome is binary:
- Pass: deploy may proceed.
- Fail: deploy is blocked (or routed to an explicit “break-glass” path with a higher approval bar).

## Where it lives

- In the CI pipeline, before changes can be merged and/or before deployment promotion.
- Optionally mirrored as a pre-deploy gate in the delivery pipeline to protect manual hotfix paths.

## How it works (implementation-neutral)

1) Detect migrations
- Identify whether a change includes database schema modifications (migration files, DDL changes, schema diffs).

2) Run a rollback-compatibility check
- Provision a clean database instance.
- Apply the candidate migration(s).
- Run N-1 application compatibility checks against the migrated schema.

Compatibility checks should cover the paths that break in rollbacks:
- startup / health checks
- representative read queries
- representative writes (including background jobs)

3) Enforce contract rules for known irreversible operations
- Explicitly fail changes that include irreversible operations unless they are in a “contract phase” that proves safety (e.g., drop column requires evidence that no deployed binaries read it).

## What happens when it blocks a change

- The pipeline fails with a message that states the violated invariant ("N-1 cannot run against migrated schema") and the failing check.
- The change is split into phases (expand/deploy/backfill/contract) until it becomes rollback-compatible.
