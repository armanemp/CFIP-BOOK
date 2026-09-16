# 12 — Testing, Observability and Operations

## Test pyramid

Use unit tests for deterministic domain rules; contract tests for ports/events/API schemas; integration tests for database/bus/provider boundaries; end-to-end tests for critical user journeys; negative/security tests for authorization and unsafe inputs; recovery tests for failures; PIT/replay tests for temporal correctness; performance/capacity tests for scale claims.

A test that merely imports a module or checks a directory is not evidence of behavioral closure.

## Observability

Use OpenTelemetry as the common telemetry foundation. Prefer standard semantic conventions before custom attributes. Correlate traces, metrics and logs across API requests, event flows, workers, data operations, research retrieval and governed agent actions.

Telemetry is observational. It must not silently become a second correctness database.

Important realtime metrics include consumer lag, queue depth, watermark, lateness, processing latency, reconnect rate and checkpoint age. API metrics include latency distributions, errors, saturation and dependency timings.

## SLOs

Define SLI/SLO per capability and workload class. Capacity planning must state traffic assumptions, concurrency, data volume, retention, dependency limits and resource budgets. Global deployment needs regional latency and failure-domain assumptions.

## Backup and disaster recovery

For every authoritative datastore define backup mechanism, retention, restore procedure, RPO/RTO target and a tested recovery path. DR claims are invalid without restore evidence.

## Rollback

Every release and autonomous change needs an identifiable change unit and reversible path. Schema changes require compatibility strategy. Worker/event changes must account for mixed-version operation and replay.

## Security operations

Dependency updates, vulnerability handling, secret rotation, audit review, incident response and access reviews are operational capabilities, not post-launch extras.
