# Problem

Rolling deployments create mixed-version fleets. Many production systems break only during the rollout window.

A deploy rarely updates all instances at once. For a period of time, version N and N-1 will both be live and exchanging requests, events, and data. If the system’s contracts are not designed for this overlap, rollout becomes a transient outage.

## How it manifests

- Errors spike only during rollout and then disappear when rollout completes.
- Canary looks “bad” because it interacts with the stable fleet.
- Retries and dead-letter queues grow during deploy windows.
- Operators observe intermittent parsing/validation failures across services.

## Why naive CI/CD pipelines miss it

- Tests validate “N works with itself,” not “N works with N-1.”
- Staging environments often upgrade everything together, eliminating the mixed-version window.
- Compatibility is multi-directional (producer/consumer, client/server). Pipelines usually test only one direction.
