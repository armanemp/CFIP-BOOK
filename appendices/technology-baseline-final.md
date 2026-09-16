# ماتریس فناوری CFIP

| حوزه | baseline | نقش | اصل جایگزینی |
|---|---|---|---|
| API | FastAPI | HTTP/WS | فقط با evidence بهتر |
| Validation | Pydantic | contracts | domain-independent |
| ORM | SQLAlchemy 2 | transactional access | preserve domain boundaries |
| Migration | Alembic | schema evolution | reversible migration |
| OLTP | PostgreSQL | source of truth | consistency first |
| Analytics | ClickHouse | large analytical workloads | benchmark required |
| Cache | Redis | acceleration/ephemeral | never business truth |
| Events | NATS JetStream | durable event delivery | outbox required |
| Local analytics | DuckDB | research/local columnar | justified workload |
| Frontend | Next.js/React/TS | terminal UX | chart-first |
| Styling | Tailwind | UI system | design tokens/policy |
| Charts | Lightweight Charts | primary chart | semantic data from backend |
| Telemetry | OpenTelemetry | traces/metrics/log correlation | vendor-neutral |
| Containers | Docker/Compose | reproducible runtime | production deployment may evolve |

هیچ ردیف به‌تنهایی اثبات production readiness نیست؛ benchmark و operational evidence لازم است.
