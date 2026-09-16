# 08 — Platform Intelligence / Elyrava

**Elyrava** is the platform-intelligence identity used in the project. It is a cross-cutting capability, not a second domain authority.

## Universal lifecycle

`Observe → Context → Reason → Act → Verify → Learn → Audit → Safety`

Every registered capability should expose the applicable hooks. Not every domain needs identical implementations, but every omission must be explicit.

## Agent boundary

`Agent Identity → Capability → Policy Hook → Authorized Tool → Action → Evidence/Telemetry → Post-action Control`

Agents cannot bypass application policies, directly mutate SQL/infrastructure, alter safety governors or erase evidence. Tool permissions are least-privilege and capability-scoped.

## Engineering intelligence

Elyrava can support repository research, issue diagnosis, test generation, evidence gathering, code proposals, controlled sandbox execution, regression analysis and release preparation. Autonomous engineering remains bounded: changes are isolated, tested, verified, health-guarded and reversible.

## Research intelligence

Elyrava consumes the Research Intelligence Fabric rather than treating retrieved text as truth. It must preserve provenance, distinguish evidence from inference and attach citations to claims when the product contract requires them.

## Trading support

Elyrava may synthesize market evidence, explain signals, compare scenarios and support risk reasoning. It does not gain unrestricted execution authority merely because it can reason about trades.

## Learning

Learning is temporal, leakage-aware and governed. Dataset identity, evaluation revision, model identity, policy version and deployment state are distinct. Promotion requires measurable evidence and rollback.

## Multi-agent safety

Concurrent agents require authenticated role-bounded communication, shared-state integrity, disagreement handling, isolation/containment and reconstructable audit. Autonomous workers must fail closed on authorization, evidence or health failures.
