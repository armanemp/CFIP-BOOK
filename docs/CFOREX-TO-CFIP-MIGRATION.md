# CForex → CFIP Migration Matrix

CForex is the behavioral source. The migration is not a file-for-file port and does not use `cforex-platform`.

| Source capability | CFIP destination | Strategy | Evidence requirement |
|---|---|---|---|
| authentication/authorization | Identity & Access | Adapt behavior into new contracts | source tests + security tests |
| market-data ingestion | Market Data | Preserve semantics, replace transport boundary | source behavior + provider contract |
| candles/normalization | Canonical Market Data | Rewrite-Minimal | golden datasets |
| FVG lifecycle | Market Structure/FVG | Preserve audited lifecycle | regression suite |
| order blocks/liquidity | Market Structure | Preserve semantics behind domain API | fixtures + property tests |
| MTF analysis | MTF Engine | Adapt concepts, new contract | cross-timeframe fixtures |
| signal generation | Signal Engine | Adapt behavior, isolate policy | deterministic replay |
| consensus | Consensus Engine | Adapt | calibration/evidence tests |
| risk/position sizing | Risk Engine | Rewrite-Minimal around explicit account/broker inputs | numerical/property tests |
| websocket/realtime | Realtime Gateway | Adapt semantics, new transport | auth + load tests |
| compare_digest/security fixes | Security Boundary | Preserve invariant | security regression |
| demo dedupe_key | Idempotency | Preserve invariant | duplicate-event tests |
| worker logging/runtime fixes | Worker Runtime | Preserve fix | boot/integration tests |
| admin git boundary | Admin Governance | Adapt only as controlled internal capability | authorization/audit tests |
| AI/research | Elyrava | New governed subsystem | evidence + sandbox gates |

## Migration sequence
G0 source closure → contracts → canonical data → event/realtime → intelligence → research/search → risk/replay/backtest → identity/payments → terminal UI → observability/security → performance → production evidence.

## Parity rule
No claim of feature parity is accepted until behavior is represented by executable evidence. A feature can be intentionally redesigned when its old implementation conflicts with CFIP invariants, but the decision must be documented.
