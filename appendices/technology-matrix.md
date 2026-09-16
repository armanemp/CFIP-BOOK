# ماتریس فناوری و انتخاب

| لایه | baseline | دلیل | شرط نگهداری |
|---|---|---|---|
| Runtime | Python 3.14 | اکوسیستم تحلیلی و backend | stable release |
| API | FastAPI | async/API contract | load + contract tests |
| Validation | Pydantic | typed boundaries | schema compatibility |
| ORM | SQLAlchemy 2 | transaction/data access | query discipline |
| Migration | Alembic | schema evolution | forward/rollback plan |
| Transaction DB | PostgreSQL | consistency/metadata | backup/restore |
| Analytics | ClickHouse | high-volume analytical queries | benchmark |
| Cache | Redis | low-latency ephemeral state | never authoritative |
| Events | NATS JetStream | durable streams | replay/consumer tests |
| Local analytics | DuckDB | portable analytical jobs | only with measured fit |
| Frontend | Next.js 16/React/TS | terminal UX | build/E2E/a11y |
| Styling | Tailwind | consistent UI system | token governance |
| Charts | Lightweight Charts | chart-first terminal | rendering benchmark |
| Telemetry | OpenTelemetry | cross-service traces/metrics | privacy + SLO |

هیچ ردیف به معنای «اجبار ابدی» نیست؛ جایگزینی باید با ADR، migration، benchmark و rollback plan انجام شود. پروژه متن‌باز جایگزین باید در ماتریس ارزیابی جداگانه ثبت شود.
