# Solution

## Invariant

After applying any schema migration associated with a deploy, the previous production application version (N-1) must still be able to:

- read the data it expects
- write the data it produces
- complete its startup and steady-state paths

This is a rollback-compatibility invariant, not a “migration succeeded” invariant.

## Why this invariant matters under continuous change

In practice, rollbacks are triggered by many issues unrelated to the database change (bad config, saturation, dependency regressions, partial region failure). If schema changes can break N-1, the system loses its fastest recovery path.

## How to preserve rollback compatibility

Structure schema changes so that incompatibility is introduced only after all running versions have been updated.

Typical sequence (conceptual, tool-agnostic):

1) Expand: add new nullable columns/tables/indexes; allow both old and new shapes.
2) Deploy: ship code that can operate with both shapes (reads both, writes both or uses safe defaults).
3) Backfill: move data to the new shape while both versions can run.
4) Contract: remove old columns/constraints only after you can prove no production binaries depend on them.

The key property is ordering: irreversible schema changes happen last.
