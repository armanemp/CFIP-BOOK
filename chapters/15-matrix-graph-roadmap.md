# 15 — Matrix, Graph and Roadmap

## Technology/capability matrix

| Capability | Primary boundary | Preferred class | Evidence required |
|---|---|---|---|
| API | Application/API adapter | FastAPI | Contract + integration + auth |
| Transactional state | Data port | PostgreSQL | Migration + transaction + recovery |
| Analytics | Analytical port | ClickHouse | Workload benchmark + retention |
| Cache | Cache port | Redis | Bounded semantics + invalidation |
| Events | Event port | NATS JetStream | Schema + ordering + redelivery + replay |
| Local analytics | Batch adapter | DuckDB if justified | Workload benchmark |
| Search | Research/search ports | BM25 + vector + reranker | Retrieval/evidence evaluation |
| Charts | UI adapter | Lightweight Charts | UX/performance/a11y |
| Telemetry | Observability port | OpenTelemetry | Trace/metric/log verification |
| Identity | Identity port | OAuth/OIDC adapter | Auth/security tests |
| Billing | Billing port | Crypto provider adapter | Idempotency/settlement/reconciliation |
| AI | Model port | Governed provider adapters | Eval + policy + rollback |

## Dependency graph

```text
Users
  ↓
Chart Terminal / API / WebSocket
  ↓
Application Use Cases
  ↓
Domain Contracts ───────────────┐
  ↓                            │
Ports                          │
  ├─ Market Data ──────────────┤
  ├─ Research/Search ──────────┤
  ├─ Broker/Execution Support ─┤
  ├─ Model/Intelligence ───────┤
  ├─ Identity/Billing ─────────┤
  ├─ Event Bus ────────────────┤
  └─ Storage/Telemetry ────────┘
       ↓
Adapters + Infrastructure
       ↓
PostgreSQL / ClickHouse / Redis / NATS / Object Storage
```

## Implementation sequence

**Track A:** source evidence and contracts.

**Track B:** data/PIT/replay and canonical engines.

**Track C:** API/events/workers/realtime.

**Track D:** search/research intelligence.

**Track E:** frontend terminal.

**Track F:** identity, policy, billing and notifications.

**Track G:** observability, security, testing, capacity and recovery.

**Track H:** Platform Intelligence and governed autonomy.

Tracks may proceed in parallel when dependencies are explicit. Shared canonical writes are reconciled and serialized.

## Definition of done

A capability is done only when its behavior is understood, contract is explicit, implementation has a canonical owner, relevant tests pass, failure/recovery semantics are covered, provenance/security/observability are addressed, and the current repository plus documentation agree.
