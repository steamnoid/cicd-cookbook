# Failure modes

## 1) Required field introduced without default/tolerance

Scenario:
- Server version N requires a new field.
- Older clients (N-1) do not send it.

Production signal:
- 4xx increases for specific client versions/services.

Common misdiagnosis:
- “Client bug” rather than “contract tightened without versioning.”

## 2) Field removed or renamed

Scenario:
- Server version N removes or renames a response/request field.
- Older clients still depend on it.

Production signal:
- Client-side parse/validation failures; increased retries.

Common misdiagnosis:
- “Serialization bug” or “bad deploy artifact.”

## 3) Type or format change

Scenario:
- Server changes a field type/format (string→number, enum changes, timestamp format).

Production signal:
- Failures clustered to one endpoint; sometimes only on specific data.

Common misdiagnosis:
- “Corrupt data” when it is actually an incompatible schema.

## 4) Semantic change behind a stable shape

Scenario:
- Response shape stays the same, but meaning changes (units, rounding, sign, sorting, idempotency).

Production signal:
- Downstream financial calculations drift; correctness bugs rather than crashes.

Common misdiagnosis:
- “Downstream bug” rather than “contract semantics changed.”

## 5) Validation tightening breaks legitimate historical traffic

Scenario:
- Server introduces stricter validation rules.
- Some callers send values that were previously accepted.

Production signal:
- 4xx spikes correlate with new server pool.

Common misdiagnosis:
- “A bad client started sending junk,” ignoring that the server changed.
