# CFIP Book

**Canonical architecture, research, reuse and delivery book for CFIP.**

Date: 2026-09-16

CFIP is a new Python-first financial-market intelligence platform derived from the real CForex source system. CForex is the behavioral/source baseline; CFIP is the destination. The abandoned `cforex-platform` repository is explicitly excluded from the target architecture.

## What this repository is

This repository is not the CFIP runtime. It is the architecture/research control book used to make the runtime deterministic, auditable and evidence-driven.

It records:

- CForex source-study and capability preservation rules
- CFIP domain and system boundaries
- technology decisions and replaceable provider boundaries
- GitHub/open-source project discovery and reuse decisions
- capability, contract, dependency and migration matrices
- smart-search / research intelligence architecture
- security, governance, observability and release gates
- implementation sequencing and evidence requirements

## Core target

Python 3.14 · FastAPI · Pydantic · SQLAlchemy 2 · Alembic · PostgreSQL · NATS JetStream · Redis · ClickHouse · DuckDB · Next.js 16 · React · TypeScript · Tailwind · TradingView Lightweight Charts · OpenTelemetry.

## Reuse rule

CFIP owns domain contracts, invariants, policy and orchestration. Mature open-source projects provide replaceable capabilities behind adapters. Decisions are **Integrate**, **Adapt**, **Reference**, **Rewrite-Minimal**, or **Reject**. No project becomes CFIP's architecture merely because it exists on GitHub.

## Primary artifact

Open `index.html` for the interactive book. The machine-readable registries under `data/` are the canonical structured source for the UI and future automation.
