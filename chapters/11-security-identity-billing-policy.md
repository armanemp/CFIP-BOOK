# 11 — Security, Identity, Billing and Policy

## Security model

Use defense in depth: strong authentication, explicit authorization, least privilege, secret isolation, input validation, safe provider boundaries, rate limits, auditability, dependency hygiene and secure defaults.

Google OAuth/OIDC is an identity adapter. The domain owns user/account identity semantics, session policy and authorization decisions.

## Policy/configuration

No user-facing or operationally meaningful behavior should depend on scattered hardcoded values. Every configurable value needs owner, type, default, allowed range/enum, environment/deployment boundary, audit policy and test coverage.

Secrets belong in secret-management boundaries, never source code, frontend bundles or ordinary configuration records.

## Entitlements

Authorization answers “may this principal perform this action?” Entitlement answers “does this account have the paid/product capability?” These are separate checks and must be composed explicitly.

## Crypto-only subscription lifecycle

`checkout → payment intent/address → payment observation/verification → settlement → subscription state → entitlement → activation → expiry/renewal → reconciliation`

Payment operations require idempotency, immutable event/audit identity, confirmation/finality policy, replay-safe settlement handling, reconciliation and explicit failure states. A payment provider is not the authority for CFIP entitlement semantics.

Free and Pro plans are product policy, not hardcoded UI assumptions. The exact commercial values belong to governed configuration.

## Audit

Security-sensitive actions, entitlement changes, provider changes, privileged tool use, autonomous actions and release decisions require reconstructable audit records. Audit history is append-oriented and protected from autonomous mutation.

## Threat model priorities

Prompt injection and untrusted research content; credential leakage; broken authorization; replay/deduplication failures; payment double-settlement; malicious provider responses; unsafe autonomous tools; supply-chain compromise; data-residency violations; denial-of-service and noisy-neighbor behavior.
