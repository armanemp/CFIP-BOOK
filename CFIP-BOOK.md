# CFIP Book — Canonical Architecture Reference

**Date:** 2026-09-16  
**Scope:** CFIP architecture, research intelligence, project adoption, implementation boundaries and verification.

## 1. Mission

CFIP is a Python-first, AI-native global financial-market intelligence platform built around evidence, reproducibility, real-time market context and governed intelligence. The book is the architecture reference; implementation repositories remain separate.

## 2. Source and destination

- **Source:** CForex — the existing system to study, inventory and migrate deliberately.
- **Destination:** CFIP — a clean architecture designed around explicit domains and contracts.
- **Rejected destination:** `cforex-platform` — permanently abandoned; do not use it as architecture, migration route or development baseline unless this decision is explicitly reversed.

## 3. Target stack

| Layer | Baseline |
|---|---|
| Runtime | Python 3.14 |
| API | FastAPI, Pydantic |
| Persistence | PostgreSQL, SQLAlchemy 2, Alembic |
| Events | NATS JetStream |
| Cache | Redis |
| Analytics | ClickHouse |
| Research | DuckDB where it improves local/reproducible analysis |
| Web | Next.js 16, React, TypeScript, Tailwind |
| Charts | TradingView Lightweight Charts |
| Telemetry | OpenTelemetry |
| Search | BM25 + semantic retrieval + fusion + optional reranking |

## 4. Product domains

Market data, charting, FVG/Order Block/MTF analysis, signals, consensus, backtest/replay, risk and position sizing, AI research/assistant, trading journal, outcome attribution/calibration/drift, providers/brokers, administration, identity, subscriptions and entitlements, notifications, governance, research intelligence and observability.

## 5. Architectural invariants

- Domain code depends on contracts, not vendor SDKs.
- Transactional truth lives in PostgreSQL.
- Redis is a cache/coordination layer, never the sole authority.
- Durable asynchronous work uses explicit event contracts.
- Data lineage survives every transformation.
- Search answers are evidence-backed; insufficient evidence produces uncertainty or abstention.
- Freshness budgets are explicit for time-sensitive domains.
- Privileged or autonomous changes require policy, audit, sandboxing, verification and rollback.
- No user-facing setting is silently hardcoded.
- Every release audits the whole repository, not just the feature being changed.

## 6. Book map

`matrix.html` technology/capability matrix; `graph.html` architecture dependency graph; `projects.html` reusable-project registry; `research.html` research fabric; `ai.html` intelligence architecture; `data.html` data lineage; `governance.html` governance; `security.html` security; `contracts.html` contracts; `testing.html` verification; `deployment.html` operations; `frontend.html` terminal UX; `trading.html` trading domain; `payments.html` billing; `observability.html` telemetry; `adoption.html` adoption workflow; `architecture-decisions.html` ADRs.

## 7. Completion rule

The book is complete only when every major architecture decision has an owner domain, contract boundary, evidence source, verification method and rollback/recovery story. Machine-readable registries in `data/` are the source for interactive views.
