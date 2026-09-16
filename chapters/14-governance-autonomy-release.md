# 14 — Governance, Autonomy and Release

## Gate 0

Gate 0 permits controlled target engineering while production promotion remains locked. Every implementation slice must be source-evidenced, contract-first, reversible, independently testable and linked to capability/test/change evidence.

## D1–D11 closure

- **D1 API/WS:** route → caller → use case → port → auth → entitlement → side effects → tests → telemetry.
- **D2 Events:** producer → outbox → subject → consumer → ordering → idempotency → retry/DLQ → projection → replay.
- **D3 Data/PIT:** schema → owner → producer → revision → dataset identity → PIT reconstruction → replay → integrity.
- **D4 Engines:** canonical identity → descriptor → implementation → registry → projection → fixtures/tests → PIT/replay → composition.
- **D5 Workers:** entrypoint → config → subscription → ownership → concurrency → checkpoint → retry → health → telemetry → recovery.
- **D6 Frontend:** route → feature → state → API/realtime → auth → UX states → i18n/a11y → telemetry → tests.
- **D7 Tests:** unit → contract → integration → E2E → negative/security → recovery → PIT/replay → performance.
- **D8 Policy/config:** hardcodes → classification → owner → flag/config → entitlement → secret boundary → deployment → tests.
- **D9 Adapters:** provider → port → config → health → retry/timeout → security → lifecycle tests.
- **D10 Operations:** SLO/SLI → capacity → retention → backup/restore → DR → rollback → residency → security → observability.
- **D11 Reconciliation:** source evidence ↔ registry ↔ parity ↔ target manifest ↔ ADRs ↔ gate register ↔ repository.

## Autonomous action contract

`identity → capability → policy → authorized tool → action → evidence → verification → post-action health/rollback`.

Agents cannot modify their own governor, safety controls or evidence history. High-impact actions require stronger gates and human approval where the product policy requires it. Disagreement among agents is a safety signal, not permission to choose an arbitrary answer.

## Release lifecycle

`Mapped → Contracted → Implemented → Verified → Parity-Verified → Production-Ready`.

Release readiness requires clean relevant CI, security checks, data/replay evidence, operational recovery, observability, performance evidence and documentation reconciliation. A green CI job does not prove parity.

## Change governance

Architecture decisions belong in ADRs. Correct an existing logical migration in place rather than accumulating duplicate corrective migrations. Canonical owners must be singular. Applied, Verified and Open states must never be conflated.
