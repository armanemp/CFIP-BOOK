# 13 — Global Scale, Resilience and Cost

Global scale is an architecture constraint from day one, but every claim requires evidence.

## Regional model

Use stateless regional APIs where workload permits. Route users/workspaces to an appropriate region. Keep data-residency boundaries explicit. Classify each replicated dataset as authoritative replication, read scaling, disaster recovery or analytical copy.

## Partitioning

Partition streams and workers by stable ownership keys. Checkpoints/leases must make ownership explicit. Consumers are deterministic and idempotent. Rebalancing cannot corrupt ordering assumptions.

## Isolation

Separate control-plane traffic, realtime traffic, analytical queries, heavy research ingestion, model evaluation and background workloads. Use quotas and fair-use controls to prevent one tenant or workload from exhausting shared capacity.

## Caching

Caches are bounded and have explicit authority/invalidation semantics. A cache miss must not silently change business meaning. Cache stampedes, stale data and eviction behavior are tested.

## Backpressure and graceful degradation

Set queue/concurrency budgets and dependency timeouts. Shed or defer non-critical work under overload. Preserve correctness-critical writes and audit events. Make degraded states observable to users and operators.

## Consistency

Every cross-region operation must declare its consistency class: strong/transactional, eventual, asynchronous replicated, analytical, or DR-only. Never infer consistency from infrastructure topology.

## Cost-aware scaling

Measure CPU, memory, storage, network, database connections, event volume, research retrieval cost and model inference cost. Optimize the bottleneck after establishing a baseline. Cost controls must not weaken PIT correctness, auditability, security or recovery.
