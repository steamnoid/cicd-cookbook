# Failure modes

## 1) Canary regression is diluted in aggregate metrics

Scenario:
- Canary is small.
- The new release has a large latency/error regression.
- Aggregated SLIs stay near baseline, so the rollout continues.

Production signal:
- Only after broad rollout does global SLI move.

Common misdiagnosis:
- “Canary didn’t catch it” rather than “we weren’t measuring canary separately.”

## 2) Rollback decision is delayed

Scenario:
- A regression starts after deploy.
- There is no reliable per-version breakdown.
- Teams spend time debating whether the deploy is causal.

Production signal:
- Time from regression start → rollback grows; RCA timeline shows long hypothesis churn.

Common misdiagnosis:
- “We need better on-call” instead of “we need release-attributed telemetry.”

## 3) False blame on dependencies

Scenario:
- A dependency also has noise or an unrelated event.
- Without segmentation, correlation is ambiguous.
- The release is blamed (or not blamed) incorrectly.

Production signal:
- Mitigation focuses on the wrong system; rollback may not help.

Common misdiagnosis:
- “Dependency outage” or “traffic shift” when the regression is version-specific.

## 4) Log search and trace sampling hide the canary

Scenario:
- Logs don’t include release id; traces don’t include release attributes.
- Sampling favors high-volume stable traffic.
- Canary evidence is effectively invisible.

Production signal:
- Engineers can’t find representative canary traces/logs without manual node-level access.

Common misdiagnosis:
- “Tracing is broken” rather than “release attributes are missing and sampling isn’t stratified.”

## 5) Metric labels explode when teams improvise

Scenario:
- Teams add ad-hoc high-cardinality labels to “get version” quickly.
- Observability cost spikes; backends throttle or drop data.

Production signal:
- Metric backend complaints, increased cost, dropped series, missing dashboards.

Common misdiagnosis:
- “Our metrics vendor is expensive” rather than “we need a bounded release identity strategy.”
