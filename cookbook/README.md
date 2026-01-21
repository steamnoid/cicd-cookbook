# CI/CD Cookbook

This cookbook is a set of production-derived CI/CD patterns. Each entry exists because it prevents a specific failure mode.

## Categories

### contract-tests

- [backward-compatible-api-changes](contract-tests/backward-compatible-api-changes/README.md)
- [mixed-version-tolerance-check](contract-tests/mixed-version-tolerance-check/README.md)

### observability-feedback

- [release-segmented-telemetry](observability-feedback/release-segmented-telemetry/README.md)

### progressive-delivery

- [deployment-block-on-slo-breach](progressive-delivery/deployment-block-on-slo-breach/README.md)

### rollback-safety

- [rollback-safe-schema-changes](rollback-safety/rollback-safe-schema-changes/README.md)
