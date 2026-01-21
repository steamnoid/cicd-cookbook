# Tradeoffs

## What this pattern makes harder

- Rapid, non-versioned interface changes become difficult; contracts must be explicit.
- Some interfaces require building test harnesses (client corpora, schema fixtures, golden messages).

## What it slows down

- Promotion speed if the contract suite is slow or has high setup cost.
- Delivery of breaking changes, which must be phased or versioned.

## When NOT to use

- Systems that deploy atomically with no mixed-version window (rare) and can prove it operationally.
- Interfaces that are entirely internal and never cross version boundaries (also rare; validate before excluding).

## Failure mode of overuse

If the suite is too broad or flaky, teams will ignore it or introduce brittle allowlists. That turns a safety gate into noise.
