# Solution

## Invariant

A service may not ship an API contract that breaks existing callers.

The protected invariant is: last promoted callers (N-1) must continue to succeed against the new server (N) for the declared compatibility surface.

## Why this invariant matters under continuous change

Independent deploy timelines create unavoidable skew. If server changes require coordinated same-day upgrades across teams, delivery velocity collapses or outages increase.

## What “backward compatible” means (contract-level)

Compatibility rules should be explicit and testable. Typical rules:

- Adding optional fields is compatible.
- Removing fields is breaking.
- Changing a field type is breaking.
- Tightening validation is breaking unless old behavior is preserved or versioned.
- Semantic changes require versioning or explicit compatibility guarantees.

If breaking change is necessary, it must be introduced via explicit versioning (new endpoint, new route version, new schema version) so old clients continue to work.
