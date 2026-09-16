# 04 — Technology and Open-Source Reuse

Technology is selected by workload and evidence, not fashion.

| Area | Baseline | Ownership rule |
|---|---|---|
| Runtime | Python 3.14 | Domain-first, typed, async where justified |
| API | FastAPI + Pydantic | Inbound adapter; contracts remain domain-owned |
| ORM/migrations | SQLAlchemy 2 + Alembic | Transactional state; explicit migrations |
| Transactional DB | PostgreSQL | Default authoritative control/business state |
| Analytics | ClickHouse | High-volume analytical/time-series workloads |
| Cache | Redis | Bounded cache/coordination; never sole authority |
| Messaging | NATS JetStream | Typed durable events, replay and consumer semantics |
| Local analytics | DuckDB | Optional, evidence-based local/batch workload |
| Web | Next.js 16 + React + TypeScript | Experience layer |
| Styling | Tailwind | Presentation only |
| Charts | TradingView Lightweight Charts | Visualization; no domain semantics |
| Telemetry | OpenTelemetry | Standard traces/metrics/log correlation |

## Open-source adoption method

Search GitHub and upstream sources deeply before implementing infrastructure that already has a mature solution. For each candidate record: repository, license, activity, release cadence, issue health, security posture, dependencies, runtime model, scalability, persistence semantics, extensibility, API stability, documentation, test quality, bus factor, operational burden and CFIP fit.

### Decision classes

- **Integrate:** use upstream directly behind a CFIP-owned port.
- **Adapt:** wrap or configure upstream with a thin integration layer.
- **Reference:** use ideas/contracts/patterns without runtime dependency.
- **Rewrite-Minimal:** implement only the small domain-specific missing surface.
- **Reject:** poor fit, unsafe license, abandoned maintenance, excessive coupling or redundant capability.

Never import an external project's internal domain model into CFIP as an authority. Never add a dependency only to improve a technology count.

## Candidate capability families

Search should cover: workflow/orchestration; event streaming; search and BM25; vector retrieval; reranking; document parsing; HTML extraction; feed/RSS; browser automation where justified; market-data libraries; technical-analysis primitives; backtesting; feature stores; model evaluation; experiment tracking; OpenTelemetry tooling; policy engines; OAuth/OIDC; billing/crypto settlement integration; notification providers; charting; localization; testing and load generation.

The selected projects and exact versions belong in the machine-readable registry and must be revalidated before adoption because upstream status changes.
