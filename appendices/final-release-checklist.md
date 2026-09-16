# چک‌لیست نهایی کتاب و release

## معماری
- [ ] bounded contextها owner و contract دارند
- [ ] canonical engineها مشخص‌اند
- [ ] data ownership مشخص است
- [ ] event ownership و idempotency مشخص است

## Data/PIT
- [ ] event/publication/availability/ingestion time تفکیک شده
- [ ] revision policy مشخص است
- [ ] dataset manifest وجود دارد
- [ ] replay deterministic است

## Product
- [ ] chart-first UX
- [ ] i18n و RTL/LTR
- [ ] accessibility
- [ ] stale/partial/error states
- [ ] notification deduplication

## Security
- [ ] authentication
- [ ] authorization
- [ ] entitlement
- [ ] secret boundary
- [ ] audit
- [ ] prompt/tool security

## Billing
- [ ] intent
- [ ] settlement/finality
- [ ] idempotency
- [ ] reconciliation
- [ ] expiry/renewal

## AI
- [ ] model/dataset provenance
- [ ] evaluation
- [ ] tool policy
- [ ] sandbox
- [ ] health guard
- [ ] rollback

## Operations
- [ ] SLO/SLI
- [ ] capacity benchmark
- [ ] backup/restore test
- [ ] RPO/RTO
- [ ] dependency/security audit
- [ ] release evidence

## Repository
- [ ] no zero-byte/marker-only operational files
- [ ] no accidental hardcodes
- [ ] docs synchronized
- [ ] decision/evidence registers synchronized
