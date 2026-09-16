# 06 — Market Data, PIT, Replay and Engines

Market intelligence is only trustworthy when historical reasoning can be reconstructed without future leakage.

## Data identity

Keep these identities distinct but linked:

- raw/provider observation identity;
- normalized market-data revision;
- dataset identity/version;
- point-in-time reconstruction identity;
- replay-case identity;
- learning/evaluation revision.

Every durable dataset has an owner, schema/version, provenance, retention, access policy, integrity mechanism and recovery policy.

## Point-in-time semantics

A PIT query must answer: what information was knowable at decision time T? It must account for event time, publication/availability time, revisions, late arrivals and correction history. A later correction must not retroactively contaminate a historical simulation unless the simulation explicitly models that information becoming available then.

## Replay

Replay uses an immutable case definition plus deterministic data identity and clock semantics. Live, replay and backtest paths should share canonical analytical semantics while using separate execution adapters. Differences must be explicit and tested.

## Engine identity

Canonical engine registry key: `(engine_id, version)`.

Each engine needs descriptor, input schema, output schema, invariants, implementation, fixtures, deterministic tests, runtime projection, durable projection where required, PIT/replay behavior and composition evidence.

### Examples of analytical families

FVG lifecycle; Order Block/market structure; multi-timeframe aggregation; indicators; signals; consensus; risk calculations; outcome attribution; calibration/drift features.

### FVG lifecycle contract

An FVG implementation must define formation, qualification, invalidation/fill, lifecycle transitions, timeframe context, ordering and boundary conditions. It must not be duplicated across workers, API handlers, replay code and frontend utilities.

## Integrity

Use sequence/watermark rules, deduplication, event-time policy, lateness handling and immutable evidence where needed. Data correctness outranks throughput.
