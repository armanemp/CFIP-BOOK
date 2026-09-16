# 02 — Evidence-Driven Source Study

CForex is the behavioral evidence base. CFIP must not infer behavior from folder names, README text or historical progress reports when executable evidence is available.

## Evidence precedence

1. Executable implementation and tests
2. Migrations, schemas and machine-readable contracts
3. Runtime composition, adapters and production entrypoints
4. CI, configuration and operational scripts
5. Architecture documentation
6. Release prose and history

## Closure chain

`artifact/schema → producer → consumer → composition → entrypoint → test → telemetry/recovery → end-to-end lifecycle`

## Evidence states

- **CONFIRMED:** directly demonstrated.
- **PARTIAL:** important dimensions proven, closure incomplete.
- **UNVERIFIED:** plausible but not executablely demonstrated.
- **NEGATIVE-SEARCH:** bounded search found no evidence; this never proves absence.
- **TARGET-REQUIRED:** source evidence establishes an obligation not yet implemented/verified.

## Migration unit

`source evidence → capability → behavioral contract → domain model → use case → port → adapter → data contract → event contract → API/UI contract → tests → parity evidence → production readiness`

The target structure may diverge from source structure when behavior and contracts are preserved and the architectural divergence is explicitly justified.

## Capability lifecycle

`MAPPED → CONTRACTED → IMPLEMENTED → VERIFIED → PARITY-VERIFIED → PRODUCTION-READY`

No stage is skipped. Gate 0 permits controlled, reversible engineering while production promotion remains locked until the applicable evidence closes.

## Source-study checklist

For each capability identify inputs, outputs, invariants, state transitions, error behavior, timing, persistence, event emission, authorization, entitlement, configuration, external providers, tests, observability, recovery and user-visible semantics. Record both positive evidence and bounded negative searches.
