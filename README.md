# CFIP Ecosystem Architecture Book

**CFIP — CForex Intelligence Platform**

این مخزن مرجع معماری، ماتریس فناوری، قراردادها، دامنه‌ها، پروژه‌ها، گراف وابستگی، استقرار، امنیت، مشاهده‌پذیری، Frontend، Trading، AI/Elyrava، Research Intelligence، Payments، Testing و Autonomy برای CFIP است.

## اصل مهم

این کتاب بر اساس **CForex واقعی به‌عنوان منبع مطالعه و مهاجرت** و معماری مقصد جدید CFIP شکل می‌گیرد. مخزن/مسیر قدیمی `cforex-platform` مبنای معماری مقصد نیست و در این کتاب به‌عنوان مسیر مهاجرت استفاده نمی‌شود.

## ساختار

```text
CFIP-Ecosystem-Architecture-Matrix/
├── index.html
├── matrix.html
├── projects.html
├── graph.html
├── contracts.html
├── adoption.html
├── deployment.html
├── governance.html
├── domains.html
├── research.html
├── trading.html
├── ai.html
├── data.html
├── security.html
├── observability.html
├── frontend.html
├── payments.html
├── testing.html
├── autonomy.html
├── architecture-decisions.html
├── README.md
├── CHANGELOG.md
├── assets/
│   ├── style.css
│   └── app.js
└── data/
    ├── domains.json
    ├── capabilities.json
    ├── projects.json
    ├── contracts.json
    ├── architecture.json
    ├── dependencies.json
    ├── decisions.json
    └── gates.json
```

## Technology baseline

- Backend: Python 3.14, FastAPI, Pydantic, SQLAlchemy 2, Alembic
- Events: NATS JetStream
- Data: PostgreSQL, ClickHouse, Redis, object storage, DuckDB for local/research analytics where appropriate
- Search: OpenSearch with BM25 + vector/hybrid retrieval, measured fusion and reranking
- Frontend: Next.js 16, React, TypeScript, Tailwind, TradingView Lightweight Charts
- Observability: OpenTelemetry traces/metrics/logs
- Intelligence: provider-neutral LLM gateway + governed Elyrava runtime
- Security: least privilege, explicit policy, provenance, audit, supply-chain controls

## Smart Search reference

The retrieval plane is intentionally multi-stage:

`Query → Planner → Lexical + Vector → Fusion/RRF or measured normalization → Reranker → Evidence → Synthesis → Citation verification`

The architecture records OpenSearch hybrid retrieval, RRF and reranking as supported implementation options; final parameters are selected only after workload-specific relevance and latency evaluation.

## Release gates

Every release is audited as a whole repository. Gates cover imports/runtime, empty or operationally empty files, security, performance, frontend accessibility/SEO/PWA/responsiveness, data integrity, search quality, AI governance, observability, migration safety and rollback.

## Autonomy policy

Elyrava may observe, diagnose, research, propose, sandbox, test and generate evidence. Production promotion and high-impact actions are governed by policy, health gates, approval requirements and rollback. Low-risk automation is permitted only when the relevant action class explicitly allows it.

## Current state

This repository is now the **CFIP Ecosystem Architecture Book foundation**. The pages are intentionally standalone and dependency-light so they can be opened directly from GitHub Pages/static hosting without a build system.
