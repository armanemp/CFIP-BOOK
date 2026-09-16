# CFIP Book

## CForex Intelligence Platform — Engineering, Architecture, Research and Reuse Guide

**Edition:** 1.0 · **Date:** 2026-09-16

This is the standalone engineering book for CFIP. It consolidates the project decisions developed in the preceding architecture/research discussions: source-study, target architecture, open-source reuse, smart search, market-data/PIT/replay, engines, trading intelligence, Platform Intelligence, API/events/workers, chart-first frontend, security, identity, crypto billing, testing, observability, global scale, autonomy and release governance.

### Non-negotiable identity

- `armanemp/CForex` is the behavioral/source baseline.
- `armanemp/CFIP` is the target implementation.
- `cforex-platform` is abandoned and excluded from the architecture.
- This repository is the book/control artifact, not the runtime.

### Target baseline

Python 3.14 · FastAPI · Pydantic · SQLAlchemy 2 · Alembic · PostgreSQL · ClickHouse · Redis · NATS JetStream · DuckDB where justified · Next.js 16 · React · TypeScript · Tailwind · TradingView Lightweight Charts · OpenTelemetry.

### Reuse principle

Do not rebuild mature infrastructure merely because it is possible. Discover current GitHub/open-source projects, evaluate maturity/licensing/security/maintenance/performance/fit, then classify each candidate as **Integrate, Adapt, Reference, Rewrite-Minimal, or Reject**. CFIP retains ownership of domain contracts, invariants, policy, provenance and orchestration.

### Progress principle

A verified capability is the unit of progress. File counts, directory counts, document counts and invented percentages are not evidence.
