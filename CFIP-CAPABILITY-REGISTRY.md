# CFIP — Capability Registry مستقل

**نسخه:** 2026-09-16  
**نقش:** فهرست canonical قابلیت‌های مطلوب CFIP  
**مقصد:** `armanemp/CFIP`  
**منبع کشف قابلیت:** `armanemp/CForex` + نیازمندی‌های معماری CFIP  
**معماری/پیاده‌سازی:** مستقل و CFIP-native

## 1. هدف

این سند فقط پاسخ می‌دهد که **CFIP چه قابلیت‌هایی باید داشته باشد**. این سند migration plan نیست و هیچ implementation، directory structure، dependency یا معماری CForex را به CFIP تحمیل نمی‌کند.

CForex فقط به‌عنوان یک **capability discovery source** استفاده می‌شود تا قابلیت‌های ارزشمند و نیازمندی‌های محصول فراموش نشوند.

قاعده:

`CForex evidence → Capability → CFIP requirement → Independent CFIP design → Contract → Implementation`

نه:

`CForex code → copy/migrate → CFIP`

`cforex-platform` نیز کاملاً خارج از این مدل است.

## 2. وضعیت‌ها

- `DISCOVERED` — قابلیت شناسایی شده.
- `SPECIFIED` — هدف و acceptance criteria مشخص شده.
- `CONTRACTED` — contract/port CFIP مشخص شده.
- `IMPLEMENTED` — implementation واقعی در CFIP وجود دارد.
- `VERIFIED` — تست/evidence معتبر دارد.
- `PRODUCTION-READY` — release gates را گذرانده.
- `RETIRED` — عمداً از scope حذف شده.

وضعیت implementation هر capability باید از repository واقعی `armanemp/CFIP` استخراج شود؛ وجود نام در این registry به معنی implementation نیست.

---

# 3. Capability Domains

## CAP-01 — Market Data

- Real-time tick/quote data
- OHLC/OHLCV
- Historical market data
- Bid/ask/spread
- Order book/depth در صورت provider support
- Volume و volume-derived metrics
- Multi-provider ingestion
- Provider health/status
- Provider fallback
- Symbol/instrument normalization
- Data quality checks
- Gap detection
- Duplicate detection
- Correction/revision handling
- Market session/calendar handling

## CAP-02 — Instrument & Market Identity

- Canonical instrument identity
- Symbol aliases
- Base/quote assets
- Asset class
- Venue/provider identity
- Contract metadata
- Pip/tick size
- Contract size
- Currency conversion
- Trading sessions
- Timezone/calendar
- Instrument lifecycle

## CAP-03 — Historical Truth / PIT

- Point-in-Time datasets
- `event_time`
- `publication_time`
- `available_at`
- `ingested_at`
- Provider revisions
- Dataset snapshots
- Historical corrections
- As-of queries
- Reproducible research snapshots
- Leakage prevention
- Replayable data manifests

## CAP-04 — Market Structure

- Swing/high-low structure
- Trend structure
- Break of Structure
- Change of Character
- Liquidity zones
- Equal highs/lows
- Support/resistance
- Supply/demand
- Displacement
- Imbalance
- Structure invalidation

## CAP-05 — FVG

- FVG candidate detection
- FVG formation
- Qualification
- Activation
- Mitigation/fill tracking
- Partial fill
- Invalidation
- Expiration/archive
- Multi-timeframe FVG
- FVG evidence/context
- FVG lifecycle replay

## CAP-06 — Order Block

- Candidate detection
- Origin candle/block
- Displacement relationship
- Qualification
- Validation
- Mitigation
- Partial mitigation
- Invalidation
- MTF relationship
- Evidence/context

## CAP-07 — MTF Analysis

- Multiple timeframe aggregation
- Timeframe alignment
- Higher-timeframe context
- Lower-timeframe trigger
- Cross-timeframe evidence
- Timeframe conflict detection
- Timeframe freshness
- Deterministic MTF replay

## CAP-08 — Indicators & Technical Analysis

- Standard indicators
- Custom indicators
- Indicator composition
- Indicator parameters
- Versioned indicator definitions
- Deterministic calculations
- Multi-timeframe indicators
- Indicator caching
- Indicator provenance
- Technical-analysis libraries/adapters

## CAP-09 — Signals

- Signal generation
- Signal lifecycle
- Direction
- Entry condition
- Trigger
- Invalidation
- Stop loss
- Take profit
- Risk budget
- Confidence
- Freshness
- Signal provenance
- Signal notification

## CAP-10 — Consensus

- Multi-signal aggregation
- Weighted voting
- Evidence weighting
- Independence estimation
- Conflict detection
- Agreement/disagreement
- Confidence aggregation
- Freshness weighting
- Regime-aware weighting
- Explainable consensus

## CAP-11 — Final Market Decision

- Direction
- Entry zone/trigger
- Stop loss
- Targets
- Invalidation
- Risk budget
- Position size
- Leverage constraint
- Confidence
- Evidence/citations
- Timeframe
- Freshness timestamp
- Scenario alternatives

**Execution authority remains separate from analytical decision output.**

## CAP-12 — Risk & Position Sizing

- Account equity
- Available balance
- Broker leverage
- Margin
- Risk-per-trade
- Fixed/variable risk budget
- Stop-distance sizing
- Position sizing
- Pip value
- Contract size
- Currency conversion
- SL/TP calculation
- Margin constraint
- Exposure limits
- Portfolio concentration
- Drawdown controls
- Kill switch

## CAP-13 — Portfolio & Exposure

- Open positions
- Pending orders
- Exposure aggregation
- Currency exposure
- Correlation exposure
- Portfolio risk
- Margin utilization
- Leverage utilization
- Concentration limits
- Scenario stress

## CAP-14 — Backtest

- Historical strategy backtest
- Event-driven simulation
- Vectorized research
- Fees
- Spread
- Slippage
- Liquidity constraints
- Execution assumptions
- Partial fills
- Position sizing
- Portfolio accounting
- Walk-forward
- Parameter evaluation
- Out-of-sample evaluation
- Reproducible result artifacts

## CAP-15 — Replay

- Market replay
- Strategy replay
- Signal replay
- FVG/OB replay
- Event ordering
- Deterministic clock
- Snapshot restore
- Replay manifest
- Replay-to-live parity checks

## CAP-16 — Paper / Simulated Trading

- Simulated orders
- Simulated fills
- Execution latency
- Slippage simulation
- Fees
- Position accounting
- Broker rule simulation
- Paper/live isolation

## CAP-17 — Live Execution

- Order submission
- Order state machine
- Cancel/replace
- Fill events
- Partial fills
- Reconciliation
- Broker connection health
- Idempotency
- Kill switch
- Live/paper isolation
- Execution audit

## CAP-18 — Trading Journal

- Manual journal entries
- Signal-linked journal
- Trade-linked journal
- Screenshots/artifacts
- Setup classification
- Emotion/context fields where user chooses to record them
- Tags
- Notes
- Outcome linkage
- Search/filter
- Journal analytics

## CAP-19 — Outcome Attribution

- Signal outcome
- Strategy outcome
- Indicator contribution
- Consensus contribution
- FVG/OB contribution
- Entry quality
- Exit quality
- Slippage impact
- Fee impact
- Risk-budget adherence
- Attribution confidence
- Counterfactual analysis where valid

## CAP-20 — Calibration & Drift

- Confidence calibration
- Brier/log-loss style evaluation where applicable
- Prediction vs outcome
- Regime drift
- Feature drift
- Data drift
- Provider drift
- Strategy degradation
- Model drift
- Alert thresholds
- Retraining/re-evaluation triggers

## CAP-21 — Research Intelligence

- Natural-language research question
- Research planning
- Query decomposition
- Source discovery
- Web retrieval
- Document retrieval
- Market-data retrieval
- Evidence extraction
- Citation anchors
- Source freshness
- Source authority
- Contradiction detection
- Evidence synthesis
- Confidence
- Reproducibility manifest

## CAP-22 — Smart Search

- Keyword search
- BM25
- Dense retrieval
- Sparse retrieval
- Hybrid retrieval
- Vector search
- Reranking
- Temporal filtering
- Instrument filtering
- Provider filtering
- Source filtering
- Facets
- Search explainability
- Recall/precision evaluation

## CAP-23 — Document Intelligence

- PDF ingestion
- HTML ingestion
- DOCX ingestion
- XLSX ingestion
- PPTX ingestion
- OCR
- Layout extraction
- Tables
- Sections
- Blocks
- Spans
- Citation anchors
- Document hashing
- Parser/version provenance

## CAP-24 — Evidence & Provenance

- Source identity
- Artifact identity
- Evidence span
- Claim
- Support relation
- Contradiction relation
- Retrieval timestamp
- Publication timestamp
- Availability timestamp
- Content hash
- Parser version
- Transformation lineage
- Freshness
- Authority
- Confidence

## CAP-25 — AI Assistant

- Contextual market explanation
- Research assistance
- Chart explanation
- Signal explanation
- Risk explanation
- Scenario analysis
- Evidence-backed answers
- Citation validation
- User conversation context
- Tool invocation
- Structured outputs

## CAP-26 — Elyrava Intelligence

- Research planning
- Retrieval orchestration
- Evidence management
- Verification
- Contradiction analysis
- Market analysis
- Signal fusion
- Decision synthesis
- Outcome learning
- Calibration
- Memory
- Model routing
- Tool registry
- Proposal generation
- Self-diagnostics
- Sandbox experimentation

Elyrava به‌تنهایی authority برای payment، authorization یا destructive operations نیست.

## CAP-27 — Agentic Workflows

- Planner
- Decomposer
- Tool selection
- Tool execution
- State/checkpoint
- Resume
- Memory
- Human approval
- Policy enforcement
- Budget/cost control
- Timeout/retry
- Failure recovery
- Audit trail

## CAP-28 — AI Self-Development

- Observe
- Diagnose
- Hypothesize
- Propose
- Generate change
- Sandbox
- Test
- Security scan
- Benchmark
- Human approval
- Promotion
- Monitoring
- Rollback

## CAP-29 — Machine Learning

- Feature engineering
- Dataset generation
- Temporal splits
- Training
- Validation
- Model registry
- Model versioning
- Experiment tracking
- Hyperparameter optimization
- Forecasting
- Classification
- Ranking
- Anomaly detection
- Representation learning
- Explainability

## CAP-30 — Reinforcement Learning

- Environment definition
- Observation space
- Action space
- Reward definition
- Transaction costs
- Slippage
- Risk constraints
- Offline evaluation
- Simulation evaluation
- Policy versioning
- Safe promotion

## CAP-31 — Events & Streaming

- Durable events
- Schema/version
- Idempotency
- Ordering
- Retry
- Dead-letter handling
- Retention
- Replay
- Consumer groups
- Backpressure
- Event audit

## CAP-32 — Workers & Workflow

- Background jobs
- Scheduled jobs
- Long-running workflows
- Retry
- Timeout
- Checkpoint
- Resume
- Concurrency control
- Distributed execution
- Job observability

## CAP-33 — Realtime Terminal

- WebSocket
- Snapshot + delta
- Sequence numbers
- Reconnect
- Heartbeat
- Backpressure
- Deduplication
- Ordering
- Tenant isolation
- Authentication
- Real-time chart updates

## CAP-34 — Chart-First Terminal

- Full-screen chart workspace
- Candlestick chart
- FVG overlays
- OB overlays
- Indicators
- Signals
- MTF context
- Drawing tools
- Timeframe controls
- Symbol search
- Command palette
- Side rail
- Bottom bar
- Drawers/modals
- Keyboard-first interaction
- Responsive layout
- PWA
- RTL/LTR

## CAP-35 — Notifications

- Signal alerts
- Price alerts
- Risk alerts
- Execution alerts
- Research completion
- System health alerts
- User-configurable channels
- Deduplication
- Rate limiting
- Delivery status

## CAP-36 — Identity & Access

- Registration/login
- Google OAuth/OIDC
- Session management
- Account security
- Role/permission model
- Tenant isolation
- API credentials
- Audit
- Revocation

## CAP-37 — Subscription & Entitlement

- Free tier
- Pro tier
- Feature entitlements
- Usage limits
- Activation
- Expiry
- Renewal
- Grace handling
- Entitlement audit

## CAP-38 — Crypto Billing

- Checkout
- Payment intent
- Payment address/invoice
- Verification
- Settlement
- Subscription linkage
- Webhook ingestion
- Idempotency
- Reconciliation
- Refund/exception handling where supported
- Payment audit

## CAP-39 — Admin / Governance

- Provider configuration
- Broker configuration
- Feature flags/configuration
- Model/provider configuration
- Proposal queue
- Approval
- Rejection
- Archive
- Audit trail
- Policy management
- Operational controls

## CAP-40 — Data Administration

- Dataset registry
- Provider registry
- Schema registry
- Data-quality status
- Revision management
- Retention
- Archive
- Deletion workflows
- Provenance
- Reconciliation

## CAP-41 — Security

- Authentication security
- Authorization
- Secret management
- SSRF protection
- Egress control
- Input validation
- Output validation
- Prompt-injection isolation
- Sandbox isolation
- Supply-chain security
- Dependency scanning
- SBOM
- Audit logs
- Rate limiting
- Abuse controls

## CAP-42 — Observability

- Logs
- Metrics
- Traces
- Correlation IDs
- Business metrics
- Agent telemetry
- Token/cost telemetry
- Tool latency
- Evidence failures
- Citation validation
- Signal outcomes
- Policy denials
- Alerting

## CAP-43 — Reliability / Operations

- Health checks
- Readiness/liveness
- Graceful shutdown
- Retry
- Circuit breaking where needed
- Backups
- Restore
- Disaster recovery
- Capacity monitoring
- Resource limits
- Incident evidence

## CAP-44 — Testing & Verification

- Unit tests
- Contract tests
- Property tests
- Integration tests
- Component tests
- E2E tests
- Load tests
- Security tests
- Data-quality tests
- Replay tests
- PIT tests
- CForex capability parity fixtures where useful
- RAG evaluation
- Agent evaluation
- Financial outcome evaluation

## CAP-45 — Internationalization & Accessibility

- Persian
- English
- Arabic
- RTL/LTR
- Locale
- Timezone
- Date/number/currency formatting
- Multilingual search
- Multilingual documents
- Keyboard accessibility
- Screen-reader semantics
- Contrast and accessibility testing

## CAP-46 — Developer Experience

- Typed contracts
- OpenAPI
- JSON Schema
- AsyncAPI
- Code quality
- Static analysis
- Formatting/linting
- Type checking
- Pre-commit
- Documentation
- Local development
- Reproducible environments

## CAP-47 — CI/CD & Supply Chain

- CI quality gates
- Unit/integration/E2E pipelines
- Security scans
- Dependency audits
- SBOM
- Artifact provenance
- Release automation
- Migration checks
- Rollback
- Versioned documentation

## CAP-48 — Global Scale

- Horizontal API scaling
- Worker scaling
- Event-stream scaling
- Analytical scaling
- Object storage
- Regional deployment boundaries
- Data residency
- Tenant isolation
- Capacity planning
- SLOs
- Cost observability
- Disaster recovery

---

# 4. استقلال CFIP

برای هر CAP شناسه CForex فقط در صورت نیاز به traceability ثبت می‌شود و هرگز target location محسوب نمی‌شود.

هر capability در CFIP باید این مسیر را طی کند:

`Capability → User/Business Requirement → CFIP Domain → Contract → Port → Implementation → Test → Evidence`

OSS در مرحله implementation بررسی می‌شود:

`Implementation Need → OSS Candidate → Gate → Adopt/Adapt/Build`

بنابراین CForex و OSS دو ورودی مستقل به طراحی CFIP هستند و هیچ‌کدام معماری CFIP را به‌تنهایی تعیین نمی‌کنند.

# 5. معیار پیشرفت

پیشرفت با **capability-weighted closure** محاسبه خواهد شد، نه با تعداد فایل یا LOC.

برای هر CAP امتیاز lifecycle از registry و evidence واقعی repository مقصد استخراج می‌شود. تا زمان ثبت وزن رسمی و وضعیت واقعی همه CAPها، درصد کل `TBD` باقی می‌ماند.

# 6. Definition of Done برای هر Capability

یک capability زمانی `PRODUCTION-READY` است که:

1. requirement روشن باشد؛
2. domain ownership مشخص باشد؛
3. contract مشخص باشد؛
4. implementation واقعی وجود داشته باشد؛
5. tests کافی وجود داشته باشد؛
6. security بررسی شده باشد؛
7. observability وجود داشته باشد؛
8. performance/reliability evidence متناسب وجود داشته باشد؛
9. replay/PIT در صورت relevance بررسی شده باشد؛
10. documentation و ADR در صورت نیاز همگام باشند؛
11. rollback/operational behavior مشخص باشد.

# 7. اصل نهایی

**CForex به ما می‌گوید چه قابلیت‌هایی ارزش بررسی دارند؛ CFIP تصمیم می‌گیرد چگونه آن‌ها را بهتر، مستقل و مدرن پیاده کند.**
