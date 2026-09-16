# Contracts and Checklists

## API checklist
- schema versioned
- authentication and authorization defined
- entitlement checked where applicable
- use case and domain owner identified
- error semantics defined
- idempotency defined for mutations
- telemetry attached
- unit/contract/integration coverage

## Event checklist
- stable subject
- schema/version
- event identity
- producer transaction/outbox
- ordering key
- consumer idempotency
- retry and DLQ
- replay/retention policy
- telemetry

## Data/PIT checklist
- owner
- schema/revision
- provenance
- dataset identity
- availability/publication time
- PIT reconstruction test
- replay identity
- retention
- backup/restore

## Engine checklist
- canonical `(engine_id, version)`
- descriptor
- deterministic fixtures
- edge cases
- runtime projection
- replay/backtest path
- no duplicate calculation surface

## Worker checklist
- entrypoint
- config
- subscription/schedule
- ownership
- checkpoint
- idempotency
- retry
- health
- graceful shutdown
- recovery

## Frontend checklist
- chart context preserved
- loading/empty/stale/error/permission states
- realtime reconnect/gap recovery
- i18n and RTL/LTR
- accessibility
- responsive behavior
- no domain logic in UI
- telemetry

## Release checklist
- current HEADs recorded
- canonical documents re-read
- source evidence reconciled
- relevant tests/CI executed
- security checks reviewed
- PIT/replay evidence closed where relevant
- capacity/SLO evidence for scale claims
- backup/restore and rollback evidence
- documentation reconciled
- Gate 0 status preserved
- production promotion remains locked until applicable gates close
