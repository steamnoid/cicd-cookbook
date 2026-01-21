# Failure modes

## 1) Column removal breaks rollback

Scenario:
- Version N adds code that stops reading a column and ships a migration that drops it.
- A rollback to N-1 happens.
- N-1 still selects the dropped column and fails.

Production signal:
- Immediate 5xx after rollback; logs show missing column.

Common misdiagnosis:
- “Rollback is broken” or “the deploy system is flaky.”

## 2) Type narrowing breaks older writes

Scenario:
- Version N changes a column type to be narrower (e.g., int → smallint) or introduces stricter constraints.
- N-1 continues writing values that were previously allowed.

Production signal:
- Elevated database errors (constraint violation, truncation) only after rollback.

Common misdiagnosis:
- “Data is corrupt” or “a bad client is sending invalid values.”

## 3) Enum/value set expansion without mixed-version handling

Scenario:
- Version N introduces a new enum value (or equivalent check constraint) and begins writing it.
- N-1 cannot parse/handle it.

Production signal:
- Old version crashes on reads, or silently maps to an incorrect default.

Common misdiagnosis:
- “Serialization bug” or “cache poisoning.”

## 4) NOT NULL added before backfill completion

Scenario:
- Version N makes a column NOT NULL.
- Some rows remain NULL (partial backfill, failed job, long tail).
- N-1 reads those rows and fails or behaves incorrectly.

Production signal:
- Rollback triggers errors on a subset of entities; harder to reproduce.

Common misdiagnosis:
- “Partial outage in one shard/tenant” or “a data migration bug unrelated to the rollback.”

## 5) Rename without compatibility bridge

Scenario:
- Version N renames a column/table and updates the code.
- The migration doesn’t keep a compatibility bridge (e.g., view/alias/dual write).
- Rollback to N-1 expects the old name.

Production signal:
- Queries fail only on rollback; monitoring indicates database errors not app CPU/memory issues.

Common misdiagnosis:
- “ORM migration bug” rather than “rollback compatibility violation.”
