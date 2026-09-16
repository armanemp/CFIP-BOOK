# 01 — Mission, Scope and Invariants

CFIP is a global-scale, AI-native financial-market intelligence platform. The product objective is not simply to display prices or generate signals. It must turn market data, structural analysis, external research, model evidence and user context into traceable intelligence and controlled action support.

## Product surface

Core capabilities include multi-timeframe charts; Fair Value Gap and Order Block analysis; indicators and market structure; signals and notifications; backtest/replay; research ingestion and search; AI assistance; consensus; outcome attribution and calibration; trading journal; account-aware position sizing and risk; provider/broker/data administration; identity; multilingual RTL/LTR UX; crypto-only subscription and entitlement lifecycle.

## Architectural invariants

1. Domain semantics do not depend on FastAPI, Next.js, PostgreSQL or any vendor.
2. Each canonical analytical implementation has one `(engine_id, version)` identity.
3. Runtime, durable and replay forms are projections/adapters of the canonical engine, not duplicate calculation surfaces.
4. PostgreSQL owns transactional/control-plane state unless an explicit ADR changes ownership.
5. ClickHouse is for suitable analytical/time-series workloads.
6. Redis is bounded cache/coordination/ephemeral state and never the sole authority for correctness.
7. Events are typed, versioned, idempotent and observable; durable outbox precedes durable fan-out.
8. Market data is provenance-bearing, revision-aware and point-in-time reconstructable.
9. AI has no direct SQL or infrastructure authority; it acts through governed tools.
10. Autonomy cannot change its own governor, safety controls or evidence history.
11. Production/live business behavior is fail-closed until applicable gates close.
12. Global-scale claims require measurement and failure/recovery evidence.

## UX invariant

The primary user experience is a professional chart-first terminal rather than a conventional scrolling dashboard. Tools live in rails, bottom bars, drawers, menus, popups and contextual panels around the chart.

## Engineering loop

`inspect → source-study → evidence graph → detect gaps/contradictions → contract → engineer → test → verify → reconcile → document → re-read GitHub → report`
