# Problem

Breaking API changes are a high-frequency source of distributed outages.

In microservice environments, callers and servers evolve independently. A server deploy that removes or changes an API contract assumption can immediately break older callers (or break only during mixed-version rollout windows). The resulting failures are often noisy and cross-team: retries, queue buildup, and partial feature outages.

## How it manifests

- Sudden increase in 4xx/5xx from a subset of callers after a deploy.
- Rollout-time failures that disappear once all callers upgrade.
- Inconsistent behavior where some clients succeed and others fail.

## Why naive CI/CD pipelines miss it

- Tests validate only N↔N (new client + new server) rather than N-1→N.
- Staging often upgrades everything together, masking older callers.
- API breakage is not consistently represented in unit tests; it’s a system contract failure.
