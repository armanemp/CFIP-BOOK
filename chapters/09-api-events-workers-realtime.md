# 09 — API, Events, Workers and Realtime

## API contract

A route is complete only when its caller, application use case, domain contract, port, authorization, entitlement, side effects, error semantics, tests and telemetry are understood. FastAPI is an adapter, not the business layer.

Use explicit versioned schemas and stable error contracts. Validate input at boundaries and preserve domain invariants inside the domain/application layers.

## WebSocket

Realtime contracts define authentication, subscription authorization, instrument/timeframe scope, sequence numbers, event identity, ordering, deduplication, heartbeat, reconnect and resynchronization. A client must be able to detect a gap and recover rather than assume an uninterrupted stream.

## Events

Producer → transaction/outbox → NATS subject → consumer → partition/ordering → idempotency → retry/DLQ → projection → replay/retention.

Event schemas are typed and versioned. Consumers must be safe under redelivery. Durable business mutation cannot depend on a best-effort in-memory publish.

## Workers

Worker closure includes entrypoint, configuration, schedule/subscription, ownership key, concurrency, checkpoint/lease, idempotency, retry, health, telemetry, graceful shutdown and recovery. Worker scale must not create duplicate correctness authorities.

## Backpressure

Bound queues and concurrency. Monitor queue depth, consumer lag, watermark, lateness, processing latency and resource budgets. Degrade explicitly when overload occurs; never silently discard correctness-critical events.

## Recovery

Design reconnect, replay, checkpoint recovery, poison-message isolation and bounded retry from the start. Recovery behavior is part of the contract and must be tested.
