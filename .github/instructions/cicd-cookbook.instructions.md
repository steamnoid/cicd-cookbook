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
First Instruction to Copilot
Propose the first cookbook pattern, following the rules above.
Do not generate files yet.
Explain the problem it addresses and why it matters.