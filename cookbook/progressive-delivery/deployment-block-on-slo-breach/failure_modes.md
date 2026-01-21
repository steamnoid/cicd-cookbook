# Failure modes

## 1) Canary regression ignored because rollout is time-based

Scenario:
- Pipeline uses a fixed sleep/wait between stages.
- Canary causes a measurable SLO regression.
- Promotion proceeds automatically because no metric gate exists.

Production signal:
- SLO burn rate increases during canary and continues rising as rollout expands.

Common misdiagnosis:
- “Canary is noisy” rather than “promotion lacks a hard stop.”

## 2) Dashboard review is too slow

Scenario:
- A human is responsible for checking graphs.
- The rollout reaches 50–100% before the regression is recognized.

Production signal:
- Incident timeline shows degradation starting at canary, but action taken after broad rollout.

Common misdiagnosis:
- “We need better on-call training” instead of “the gate must be automated.”

## 3) Global metrics mask canary-specific impact

Scenario:
- Canary is 1–5% and global SLI averages look fine.
- Canary pool is failing badly but diluted in aggregate.
- Promotion proceeds.

Production signal:
- High error rate when filtering by canary version, but low global error rate.

Common misdiagnosis:
- “Canary was healthy” due to looking at aggregate metrics.

## 4) Wrong SLI selection creates a false-negative gate

Scenario:
- Gate uses a metric not correlated with user impact (CPU, pod restarts).
- Real regression is latency/error at the edge or critical dependency saturation.

Production signal:
- Gate passes while customer-facing SLO is violated.

Common misdiagnosis:
- “Gating doesn’t work” rather than “gate is measuring the wrong thing.”

## 5) Gate flaps due to low traffic / low sample size

Scenario:
- Canary window is short or traffic is low.
- Randomness triggers false breaches.
- Teams disable the gate.

Production signal:
- Frequent gate failures that are not correlated with incidents.

Common misdiagnosis:
- “Canary gating is impractical” rather than “needs minimum-volume and statistical handling.”
