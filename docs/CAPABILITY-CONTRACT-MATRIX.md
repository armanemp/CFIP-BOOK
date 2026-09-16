# CFIP Capability & Contract Matrix

Every capability must have: owner domain, public contract, persistence owner, event semantics, external-provider boundary, authorization policy, observability, test strategy, failure/rollback behavior and release gate.

| Area | Primary owner | Contract | Persistence | Event | Gate |
|---|---|---|---|---|---|
| Identity | Identity | AuthSession/User | PostgreSQL | identity.* | G6 |
| Entitlement | Subscription | Entitlement | PostgreSQL | entitlement.* | G6 |
| Market data | Market Data | Quote/Candle/Tick | PostgreSQL/ClickHouse | market.* | G2 |
| Structure | Intelligence | FVG/OB/Liquidity | PostgreSQL/ClickHouse | structure.* | G4 |
| Indicators | Intelligence | IndicatorResult | ClickHouse/cache | signal.* | G4 |
| Signals | Signals | Signal/Decision | PostgreSQL | signal.* | G4 |
| Consensus | Intelligence | ConsensusResult | PostgreSQL/ClickHouse | consensus.* | G4 |
| Risk | Risk | PositionSizing/RiskCheck | PostgreSQL | risk.* | G5 |
| Replay | Replay | ReplaySession/Event | ClickHouse/object data | replay.* | G5 |
| Backtest | Research | BacktestRun/Metric | ClickHouse/object data | backtest.* | G5 |
| Search | Research | SearchQuery/SearchResult | indexes | research.* | G3 |
| Evidence | Research | Evidence/Citation | PostgreSQL/object data | evidence.* | G3 |
| AI | Elyrava | ModelRequest/Response | PostgreSQL/audit | ai.* | G3/G8 |
| Notifications | Notification | Notification | PostgreSQL | notification.* | G7 |
| Broker | Execution | BrokerOrder/Execution | PostgreSQL | execution.* | G5/G10 |
| Journal | Journal | JournalEntry | PostgreSQL | journal.* | G5 |
| Audit | Governance | AuditEvent | PostgreSQL/immutable sink | audit.* | G8 |
| Admin proposals | Governance | Proposal/Approval | PostgreSQL | governance.* | G8 |
| Payments | Payments | PaymentIntent/Settlement | PostgreSQL | payment.* | G6 |
| Analytics | Analytics | Metric/Attribution | ClickHouse | analytics.* | G9 |

## Contract discipline
Commands express intent; events express facts. Event payloads are versioned. Consumers must tolerate compatible additive evolution. Idempotency is explicit for external callbacks, payment settlement and replayable event handlers.
