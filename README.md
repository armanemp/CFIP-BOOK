# CFIP Book

Canonical architecture reference for CFIP.

Date: 2026-09-16

Source system: CForex.
Destination: CFIP.

Important: cforex-platform is abandoned and is not a destination, migration route, or development baseline.

Core stack: Python 3.14, FastAPI, Pydantic, SQLAlchemy 2, Alembic, PostgreSQL, NATS JetStream, Redis, ClickHouse, DuckDB where useful, Next.js 16, React, TypeScript, Tailwind, TradingView Lightweight Charts, OpenTelemetry.

Architecture principles: explicit domain boundaries; versioned contracts; replaceable providers; PostgreSQL as transactional authority; durable events; recoverable raw data; explicit freshness; evidence-backed intelligence; tenant-aware security; whole-repository verification for every release.

The interactive book is in index.html. Supporting reference material is in docs and data directories.
