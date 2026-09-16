# CFIP Book — Complete Architecture & Research Baseline

## 1. Mission
CFIP is a global-scale, AI-native forex and financial-market intelligence platform. It must combine market data, technical structure, multi-timeframe analysis, signals, evidence, research, backtesting/replay, risk, journaling, realtime delivery, user accounts, subscriptions, administration and governed intelligence without coupling the product to one vendor or one open-source project.

## 2. Source and destination
- **Source of behavior:** CForex. Existing behavior, invariants and audited fixes are evidence to preserve.
- **Destination:** CFIP. New architecture; no Laravel/PHP dependency.
- **Excluded:** `cforex-platform` is abandoned and is not a migration baseline.
- **Intelligence name:** Elyrava.

## 3. Architectural invariants
1. PostgreSQL is system of record for transactional truth.
2. NATS JetStream is durable event transport; Redis is cache/ephemeral coordination, never authoritative truth.
3. Every external provider is behind an adapter/port.
4. Domain contracts are owned by CFIP, not copied from an OSS implementation.
5. Raw external data is immutable and provenance-aware before normalization.
6. Research results carry source, timestamp, content hash and transformation lineage.
7. High-impact autonomous changes require policy checks, sandbox execution, tests, evidence, approval and rollback.
8. Production/live trading and high-impact mutation remain gated until explicit evidence closes the relevant release gates.
9. User-facing values and settings are configuration-driven; no hardcoded product policy.
10. Frontend is chart-first terminal UX: one primary chart workspace, tools in rails/drawers/popups/bottom bars rather than dashboard sprawl.

## 4. Product domains
Identity & access; tenancy; subscriptions & entitlements; payment settlement; user preferences/i18n; instruments/symbols; market data; normalization; candles/ticks/order book; technical indicators; market structure; FVG; order blocks; liquidity; MTF; signals; consensus; scoring/calibration; alerts/notifications; chart terminal; replay; backtesting; strategies; portfolio/risk; broker accounts; execution boundary; trading journal; outcomes/attribution; research ingestion; search/indexing; hybrid retrieval; reranking; evidence/provenance; AI assistant; model gateway; prompt/tool policy; knowledge graph; datasets; evaluation; ML lifecycle; observability; audit; governance; admin proposal queue; sandbox/self-development; security; deployment; disaster recovery.

## 5. Research/reuse method
For every candidate repository record: capability, canonical URL, license, activity, release state, maintenance, architecture, language/runtime, Python compatibility, API/extensibility, test quality, security posture, dependency burden, performance/scalability, self-hosting, lock-in, documentation, integration cost, migration risk, provenance confidence and final disposition.

Disposition meanings:
- **Integrate:** use upstream as a bounded dependency/service.
- **Adapt:** use upstream capability with a CFIP adapter or constrained fork.
- **Reference:** study algorithms/patterns; do not ship as a dependency.
- **Rewrite-Minimal:** only the missing CFIP-specific contract/glue is implemented.
- **Reject:** unsuitable, stale, incompatible, risky, duplicative or license-incompatible.

## 6. Canonical architecture graph
```text
                     ┌─────────────────────────────┐
                     │       CFIP Web Terminal      │
                     │ Next.js + React + TS + TVLC │
                     └──────────────┬──────────────┘
                                    │ HTTPS/WebSocket
                           ┌────────▼─────────┐
                           │   FastAPI API    │
                           │ policy + ports   │
                           └──────┬─────┬─────┘
                                  │     │
                     ┌────────────┘     └───────────────┐
                     ▼                                  ▼
              ┌──────────────┐                  ┌──────────────┐
              │ PostgreSQL   │                  │ NATS         │
              │ system truth │                  │ JetStream    │
              └──────┬───────┘                  └──────┬───────┘
                     │                                 │
          ┌──────────┴──────────┐             ┌────────┴────────┐
          ▼                     ▼             ▼                 ▼
   transaction/risk       provenance/audit  workers        realtime fanout
          │                     │
          └──────────┬──────────┘
                     ▼
              ┌──────────────┐       ┌──────────────┐
              │ ClickHouse   │       │ Redis        │
              │ analytics    │       │ cache/limits │
              └──────────────┘       └──────────────┘
                     ▲
                     │ normalized datasets
      ┌──────────────┴─────────────────────────┐
      │ data connectors → raw → parse → dedup │
      │ → canonical docs → chunk → indexes    │
      └──────────────┬─────────────────────────┘
                     ▼
       ┌──────────────────────────────────────────┐
       │ Hybrid Research: BM25 + Vector + RRF + │
       │ optional reranker + evidence selection │
       └──────────────────┬───────────────────────┘
                          ▼
                   ┌──────────────┐
                   │ Elyrava      │
                   │ governed AI  │
                   └──────────────┘
```

## 7. Smart Search / Research Intelligence
`Query → Policy → Planner → Expansion → Lexical + Vector Retrieval → Fusion → Rerank → Evidence Selection → Synthesis → Citation Verification → Response`.

BM25 protects exact identifiers and rare terms. Dense retrieval covers semantic similarity. Fusion prevents one retrieval mode from dominating. Reranking is an independent stage. Evidence is immutable enough to reproduce a response. Freshness and contradiction checks can block synthesis. External content is untrusted input and is isolated from privileged instructions/tools.

## 8. Data plane
Connectors → immutable raw objects → parser/extractor → canonical document/event → deduplication → metadata → embeddings/features → lexical/vector indexes → analytics. Every transformation has a version and lineage record.

## 9. Control plane
Provider/model/index configuration; budgets; feature flags; tenant isolation; policy; allowlists; credentials; audit; approval queues; release manifests; evaluation sets; rollback metadata.

## 10. Security
OAuth/OIDC; secure sessions/tokens; CSRF where applicable; SSRF-safe fetching; redirect restrictions; MIME/size/time limits; sandboxed parsing; prompt-injection resistance; secret isolation; tenant authorization; rate limits; privileged audit; signed/reproducible artifacts; dependency and container scanning.

## 11. Trading and risk boundary
Market analysis can produce hypotheses and signals. Execution is a separate privileged boundary. Position sizing must use account equity, broker leverage, instrument constraints, stop loss/take profit and explicit risk policy. No AI output directly becomes a live order without the execution policy boundary.

## 12. Payments
Crypto-only Free/Pro lifecycle: checkout → intent/address → verification → settlement → subscription → entitlement → activation → expiry/renewal, with idempotency keys, audit trail, reconciliation and replay-safe state transitions.

## 13. Governance / autonomy
Elyrava may research, diagnose, propose and test changes in a sandbox. Mature suggestions enter an admin proposal queue. Promotion requires evidence, health checks and rollback. High-impact autonomous mutation is prohibited by default.

## 14. Release gates
G0 source closure; G1 architecture/contracts; G2 data plane; G3 search/research; G4 market intelligence; G5 trading/risk/replay; G6 identity/payments; G7 frontend; G8 observability/security; G9 integration/performance; G10 production readiness. Every release also runs whole-repository checks for missing/empty files, imports, runtime boot, Docker, dependencies, tests, migrations, contracts, security, performance and documentation consistency.

## 15. Definition of complete
The Book is complete only when every required capability has a domain owner, contract, dependency decision, data ownership, security classification, observability plan, test/evidence gate and implementation phase; every external project has a documented disposition or an explicit reason it is not yet researched.
