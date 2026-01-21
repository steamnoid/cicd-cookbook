cicd-cookbook.instructions.md
Purpose
This repository is a CI/CD Cookbook for Mature Systems.
It is not a tutorial.
It is not a best-practices list.
It is not a reference manual.
Each entry exists because it solves a specific, real CI/CD failure mode observed in production systems.
The cookbook is built iteratively, one problem → one pattern at a time.
Core Principle
Every automation must justify its existence by the problem it addresses.
No pattern is allowed without:
a clear failure mode
a measurable signal
a concrete guardrail
Cookbook Structure (MANDATORY)
Each cookbook entry MUST follow this exact structure:
/cookbook/
  <pattern-name>/
    README.md
    problem.md
    failure_modes.md
    solution.md
    automation.md
    metrics.md
    tradeoffs.md
No file may be skipped.
Canonical Entry Template
problem.md
Describe:
the real-world CI/CD problem
how it manifests (symptoms)
why naive CI/CD pipelines fail to catch it
NO solutions here.
failure_modes.md
List:
concrete failure scenarios
how they appear in production
what teams usually misdiagnose them as
Focus on system behavior, not tooling.
solution.md
Explain:
the architectural or process invariant being protected
why this invariant matters under continuous change
Use plain language, no buzzwords.
automation.md
Describe:
how this invariant is enforced automatically
where it lives (pipeline, runtime, deploy step)
what happens when it blocks a change
Automation must be binary: pass / fail / degrade.
metrics.md
List:
the signals this pattern introduces
how to interpret them over time
what “good” and “bad” trends look like
Metrics must drive decisions, not reporting.
tradeoffs.md
Explicitly document:
what this pattern makes harder
what it slows down
when it should NOT be used
No pattern is universally good.
Allowed Pattern Categories
Copilot may only add patterns in these categories:
guardrails/
fitness-functions/
contract-tests/
progressive-delivery/
rollback-safety/
observability-feedback/
Each pattern must live in exactly one category.

Project Context (CRITICAL)
This cookbook is being built to support a high-throughput, distributed backend platform in a regulated financial/ledger domain.
Assume:
- microservices and/or distributed components
- rolling deployments (mixed-version windows)
- strict correctness expectations (ledger-like invariants)
- privacy constraints (limited access to data; telemetry must be designed carefully)

Recruiting Alignment (CRITICAL)
When choosing the next pattern, prefer patterns that demonstrate and reinforce Senior QA / delivery ownership for distributed backend systems:
- backend/API testing in distributed or microservices environments
- test automation and CI/CD gating (binary pass/fail/degrade)
- quality metrics that drive release decisions
- release planning/coordination failure modes (promotion, rollout, rollback)

This alignment affects ordering only; it does not relax any structure, quality, or category constraints.
Pattern Naming Rules
Pattern names must:
describe the problem, not the tool
avoid vendor names
be phrased as capabilities or constraints
Good:
rollback-safe-schema-changes
mixed-version-tolerance-check
deployment-block-on-slo-breach
Bad:
kubernetes-canary
prometheus-alerts
github-actions-pipeline
Iteration Rules (CRITICAL)
Copilot must follow this loop:
Propose one new pattern
Explain why this pattern is needed
Wait for explicit approval (proceed)
Only then generate files for that pattern
No bulk generation.
No parallel patterns.

Pattern Ordering Rules (CRITICAL)
When proposing the next pattern, prefer the simplest pattern that delivers the highest risk reduction per unit of complexity.
Order patterns from:
- highest value / lowest effort
- to lower value / higher effort

Define “simplicity” concretely as:
- minimal number of moving parts to enforce the guardrail
- minimal cross-team coordination required
- minimal new runtime dependencies
- minimal operational surface area
- minimal cost to adopt and run (CI minutes, infra, vendor spend)

Implementation Bias (ORDERING ONLY)
All else equal, prefer patterns that can be enforced in CI/CD (pre-merge / pre-promotion) without introducing new always-on runtime services or long-lived operational components.

Define “value” concretely as:
- prevents a common, high-severity production failure mode
- introduces a measurable signal that changes decisions
- blocks failures before broad user impact

If two candidate patterns are similar value, choose the simpler one first.

Example First Patterns (SEED ONLY)
Copilot may start with ONE of:
rollback-safe-schema-changes
mixed-version-deploy-tolerance
contract-test-for-backward-compatibility
canary-deploy-with-metric-gating
Only one.
Quality Bar
A pattern is acceptable only if:
a senior engineer would say
“Yes, I’ve seen this exact problem in prod.”
removing the pattern would measurably increase risk
the automation would fail before users notice
If not, the pattern must be rejected.
Tone & Style
precise
pragmatic
production-oriented
no motivational language
no “best practices”
no “industry standards”
This cookbook documents earned constraints, not ideals.
End Goal
By the end, this repository should function as:
a design review reference
a CI/CD maturity checklist
a guardrail decision aid
a teaching tool for senior engineers
Not as a tutorial.
