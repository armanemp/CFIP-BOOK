# CFIP Research Registry — GitHub Discovery Method

## Purpose
This registry records open-source discovery as evidence, not as an automatic dependency list. Search is repeated across trading engines, backtesting, market data, indicators, retrieval/RAG, graph systems, financial ML, authentication, frontend/charting, observability and infrastructure.

## Required repository audit
Before any dependency is promoted into CFIP, inspect:

1. default branch and recent commit history;
2. releases/tags and release cadence;
3. declared license and third-party license obligations;
4. Python/runtime compatibility and packaging metadata;
5. dependency graph and native/system requirements;
6. test suite and CI configuration;
7. security advisories, unsafe deserialization/network behavior and secret handling;
8. public API stability and extension points;
9. performance characteristics and data-volume assumptions;
10. self-hosting and operational complexity;
11. issue/PR maintenance signal;
12. integration surface and ability to isolate behind an adapter.

## Search families completed for the current baseline
- Forex/trading platforms
- Python backtesting
- financial data pipelines
- hybrid/vector search
- RAG/GraphRAG/agent research
- financial ML/time series
- technical analysis/indicators
- exchange connectivity
- FastAPI/OAuth examples
- TradingView/chart integrations

## Important distinction
A GitHub search result is not equivalent to a technical endorsement. Candidate projects are intentionally separated into Integrate/Adapt/Reference/Evaluate/Reject. The final dependency manifest must pin exact versions or commits and preserve license/provenance evidence.

## Research backlog categories
Market-data providers/connectors; FIX/IB/OANDA/MetaTrader boundaries; Timescale/Postgres time-series options; ClickHouse ingestion; object stores; NATS tooling; workflow/orchestration; OpenTelemetry; SSO/OIDC; WebAuthn/passkeys; notification gateways; crypto payment processors; frontend chart libraries; Web Workers/WASM numerical acceleration; document parsers; embedding/reranker models; vector stores; GraphRAG; evaluation frameworks; model gateways; feature stores; experiment tracking; model registry; policy engines; sandboxing; SBOM/signing; supply-chain security.
