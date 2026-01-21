# Failure modes

## 1) New producer emits fields old consumer can’t parse

Scenario:
- Version N adds a new required field or changes a field type.
- Version N starts producing messages/events.
- Version N-1 consumers reject the payload and fail or drop messages.

Production signal:
- DLQ growth; consumer error logs show deserialization/validation failures.

Common misdiagnosis:
- “Queue is flaky” or “serializer bug in the new version.”

## 2) Old client breaks against new server validation

Scenario:
- Version N tightens request validation.
- During rollout, old clients (or old sidecars) still send the old shape.
- New servers return 4xx/5xx for otherwise valid traffic.

Production signal:
- Increased 4xx during rollout; correlation with new server pool.

Common misdiagnosis:
- “Client bug” rather than “contract change not staged for mixed-version.”

## 3) New consumer assumes producer upgraded first

Scenario:
- Version N consumer starts requiring a new event or field.
- Producers are still on N-1 during early rollout.
- The new consumer crashes or stops doing useful work.

Production signal:
- Background workflows stall; error logs indicate missing fields/events.

Common misdiagnosis:
- “Partial outage” or “dependency is down.”

## 4) Incompatible cache/serialization format across versions

Scenario:
- Version N changes cache key format or stored value encoding.
- Old and new versions share the same cache.
- Each version corrupts or invalidates the other’s entries.

Production signal:
- Elevated cache miss rate; oscillating performance; rollout-correlated latency.

Common misdiagnosis:
- “Cache cluster issue” rather than “format incompatibility.”

## 5) Database writes are forward-only during rollout

Scenario:
- Version N starts writing data that N-1 can’t read/interpret.
- While N-1 is still live, it reads the new data and fails or behaves incorrectly.

Production signal:
- Rollout-time 5xx clustered on old nodes; DB errors may be absent.

Common misdiagnosis:
- “Old nodes are unhealthy” rather than “mixed-version read incompatibility.”
