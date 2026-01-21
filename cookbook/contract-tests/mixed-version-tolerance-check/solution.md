# Solution

## Invariant

For each declared interface, version N and N-1 must interoperate during a rolling deploy.

“Interoperate” is defined by the system’s real communication paths:

- request/response APIs
- events/messages
- shared storage formats (cache, database record shape, serialized blobs)

## Why this invariant matters under continuous change

Rollouts create a temporary distributed system with skewed versions. If compatibility is not explicit and verified, deploy safety becomes dependent on rollout timing, traffic shape, and which component upgrades first.

## What mixed-version tolerance requires

- Backward compatibility where new components must accept old payloads.
- Forward tolerance where old components must ignore unknown fields/values (or handle safe defaults).
- Versioning rules that specify which side can change first (producer-first vs consumer-first).

A practical definition to enforce:

- N server must accept N-1 client requests on the same endpoint.
- N-1 server must accept N client requests that only add optional fields.
- N consumer must handle N-1 producer messages.
- N-1 consumer must ignore N producer additions that are optional or additive.

The exact rules vary per interface; the key is that they are declared and tested.
