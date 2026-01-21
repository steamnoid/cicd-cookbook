# Automation

## What is enforced

A mixed-version contract suite runs as a promotion gate.

Outcome is binary:
- Pass: change may be promoted.
- Fail: change is blocked until contracts are made mixed-version tolerant.

## Where it lives

- In CI as a required check before merge (fast feedback).
- In the delivery pipeline as a pre-promotion gate (protects hotfix and manual paths).

## How it works (implementation-neutral)

1) Define the contracts under test
- Declare which interfaces are subject to mixed-version tolerance (API endpoints, message schemas, cache formats, DB record formats).

2) Select the versions
- N: candidate build.
- N-1: last production build (or last promoted artifact).

3) Exercise both directions

API example:
- Run N server and send an N-1 client request corpus; assert success and stable semantics.
- Run N-1 server and send N client requests restricted to additive/optional changes; assert no rejection and stable semantics.

Messaging example:
- Produce messages with N producer; consume with N-1 consumer; assert no deserialization failure and correct handling.
- Produce messages with N-1 producer; consume with N consumer; assert behavior is correct.

Storage format example:
- Write with N; read with N-1 for all records that N-1 will encounter during rollout.
- Write with N-1; read with N.

4) Fail on contract breaks
- Any incompatibility fails the gate with a message pointing to the interface and direction (N→N-1 or N-1→N).

## What happens when it blocks a change

- The change is split into phases (introduce tolerant reads first, then introduce new writes).
- The interface is versioned explicitly (new endpoint/topic/schema version), making the rollout order safe.
