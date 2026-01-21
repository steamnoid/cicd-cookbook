# CI/CD Cookbook

This repository is a CI/CD cookbook for mature systems.

It is not a tutorial.
It is not a best-practices list.
It is not a reference manual.

Each cookbook entry exists because it solves a specific CI/CD failure mode observed in production.

## The “source of truth”

The core of this repo is the instructions file:

- `.github/instructions/cicd-cookbook.instructions.md`

This file is intended to **instruct GitHub Copilot (or another AI coding assistant)** how to extend the cookbook safely and consistently.

That instructions file defines:

- the mandatory entry structure
- the allowed categories
- the propose → approve (`proceed`) → generate loop
- the quality bar (failure mode, measurable signal, concrete guardrail)

If you want to generate new patterns consistently, follow the rules in that file.

## Using Copilot to generate patterns

You don’t need to hand-author entries. The intended workflow is to ask Copilot to generate them, one at a time, using the instructions file as the rulebook.

Suggested prompts:

1) Ask for a proposal (no files yet)
- “Propose the next cookbook pattern, following the rules in `.github/instructions/cicd-cookbook.instructions.md`. Do not generate files yet. Explain the problem it addresses and why it matters.”

2) Approve generation
- Reply with: `proceed`

Copilot should then create exactly one new entry under `cookbook/<category>/<pattern-name>/` and update `cookbook/README.md`.

## Where patterns live

- Index: `cookbook/README.md`
- Entries: `cookbook/<category>/<pattern-name>/`

Each entry is always a 7-file bundle:

- `README.md`
- `problem.md`
- `failure_modes.md`
- `solution.md`
- `automation.md`
- `metrics.md`
- `tradeoffs.md`

## How to generate a new pattern

This repo is intentionally optimized for iterative generation.

1) Propose exactly one pattern
- Describe the problem (symptoms) and why naive pipelines miss it.
- Name the failure modes you’re targeting.
- State the guardrail (binary) and the measurable signal.

2) Wait for explicit approval
- Do not create files until the reviewer replies with `proceed`.

3) Generate the entry
- Create exactly one new entry under one allowed category.
- Fill all required files (none may be skipped).

4) Update the index
- Add a link to the new entry in `cookbook/README.md`.

## What “good” looks like

- Production-oriented and specific: “I’ve seen this exact thing break prod.”
- Automation is enforceable: pass / fail / degrade.
- Prefer patterns that are cheap to adopt and run (CI/CD gates over new always-on runtime components), unless the added complexity is justified.
