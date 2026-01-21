# Problem

Database schema changes can silently remove the ability to roll back.

In many systems, schema changes are applied once and persist across application versions. If a new deploy changes the database in a way the previous application version cannot tolerate, then a rollback (triggered for any reason) becomes a user-impacting event.

## How it manifests

- Rollout looks healthy, but rollback causes immediate error spikes.
- Operators see failures only after traffic is shifted back to the previous version.
- Teams hesitate to roll back because they suspect it will make things worse.

## Why naive CI/CD pipelines miss it

- Pipelines validate “new version works after migration,” not “previous version still works after migration.”
- Migration steps report success (DDL applied) even when the resulting schema breaks older readers/writers.
- The failure is time-shifted: it appears during rollback, not during rollout.
