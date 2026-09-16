# CFIP — کتاب جامع معماری، مهندسی، اکوسیستم و نقشه اجرای مرجع

**نسخه:** 2026-09-16  
**وضعیت:** Canonical Architecture Book  
**مرجع مقصد:** `armanemp/CFIP`  
**منبع رفتاری/مهاجرتی:** `armanemp/CForex`  
**نام هوش پلتفرم:** Elyrava  

> این سند مرجع واحد تصمیم‌های معماری CFIP است. هر capability باید از «ادعا» به «قرارداد»، «پیاده‌سازی»، «evidence» و در نهایت «production readiness» برسد. `cforex-platform` عمداً خارج از معماری و مسیر مهاجرت است.

---

## 0. خلاصه اجرایی

CFIP یک **Financial/Forex Intelligence Platform** و یک terminal حرفه‌ای chart-first است؛ نه یک dashboard معمولی، نه صرفاً RAG، نه مجموعه‌ای از microserviceهای تصادفی و نه یک wrapper دور چند LLM.

معماری مرکزی:

`Experience → Inbound → Application → Domain → Contracts/Ports → Capability Fabric → OSS Adapters → Infrastructure`

اصل مالکیت:

**CFIP owns contracts, domain semantics, evidence, governance and differentiated intelligence; OSS owns reusable generic implementation behind explicit adapters.**

CFIP باید از CForex قابلیت‌های معتبر را استخراج و با رفتار قابل‌اثبات منتقل کند، اما معماری مقصد را مستقل نگه دارد. هر قابلیت جدید ابتدا با reuse/upstream بررسی می‌شود و فقط در صورت وجود دلیل فنی، حقوقی، performance یا domain-IP به سمت extension/fork/build حرکت می‌کند.

---

# Part I — اصول و مدل معماری

## 1. Mission و اصول غیرقابل مذاکره

1. Evidence قبل از ادعا.
2. Capability واحد سنجش پیشرفت است، نه تعداد فایل یا LOC.
3. هر مفهوم domain فقط یک semantic authority دارد.
4. Point-in-time correctness برای research، backtest، ML و outcome analysis اجباری است.
5. Business event مهم ابتدا durable می‌شود؛ سپس fan-out.
6. Redis منبع حقیقت business نیست.
7. Policy و authorization بیرون از agent و model قرار دارند.
8. Configuration و policy باید data-driven و قابل audit باشند.
9. مسیرهای حساس fail-closed هستند.
10. destructive change باید reversible باشد.
11. external web/GitHub/PDF/news ورودی untrusted است و می‌تواند prompt injection داشته باشد.
12. production فقط با stable releases؛ prerelease/nightly/canary برای baseline ممنوع.
13. هیچ OSS project صرفاً به‌خاطر شهرت وارد runtime نمی‌شود.
14. هیچ capability با چند implementation موازی و متناقض در production پذیرفته نیست.
15. همه ادعاهای scale باید benchmark، SLO، capacity و cost evidence داشته باشند.
16. انسان در تصمیم‌های high-impact کنترل نهایی را حفظ می‌کند.

## 2. مدل capability lifecycle

`MAPPED → CONTRACTED → IMPLEMENTED → VERIFIED → PARITY-VERIFIED → PRODUCTION-READY`

وضعیت‌های evidence:

- **CONFIRMED:** مسیر اجرایی و تست کافی.
- **PARTIAL:** بخشی از capability موجود است.
- **UNVERIFIED:** artifact یا ادعا وجود دارد ولی closure ندارد.
- **NEGATIVE-SEARCH:** با جست‌وجوی مشخص پیدا نشد.
- **TARGET-REQUIRED:** برای معماری مقصد لازم است.
- **DEPRECATED:** عمداً حذف یا جایگزین شده.

Evidence hierarchy:

`executable test > runtime composition > schema/contract/migration > CI/ops evidence > documentation > claim`

---

# Part II — 30 حوزه مرجع CFIP

## 3. Domain 01 — Forex / Trading / Quant Core

Capabilityها: market data, tick, OHLCV, order book, microstructure, technical analysis, price action, market structure, liquidity, FVG, Order Block, supply/demand, S/R, MTF, patterns, indicators, signals, strategy engine, backtest، event-driven backtest، walk-forward، replay، paper/live، execution، slippage، transaction cost، portfolio، sizing، leverage، margin، SL/TP، trade management، journal و attribution.

**Reuse candidates:** NautilusTrader، LEAN، Qlib. این پروژه‌ها فقط engine capability می‌دهند؛ semantic IP مثل FVG/OB، signal fusion، confidence و market-intelligence reasoning متعلق به CFIP است.

## 4. Domain 02 — Market & Financial Data

Forex/broker/exchange feeds، economic calendar، central banks، rates، macro، COT، news، sentiment، alternative/fundamental، historical/tick، streaming، normalization، correction، quality، filings و cross-asset.

Candidates: yfinance، OpenBB، Nasdaq Data Link tooling، Stooq، Alpha Vantage integrations، FMP integrations، Polygon/Massive integrations، ccxt، pandas-datareader، fredapi، sec-edgar-downloader، edgartools، Arelle/XBRL، databento tooling و exchange clients.

Provider نباید وارد domain model شود؛ قراردادهای `MarketDataProvider`, `EconomicDataProvider`, `NewsProvider`, `FundamentalDataProvider` مرز هستند.

## 5. Domain 03 — Trading Engine & Execution

Broker/exchange adapters، FIX، REST/WebSocket، order lifecycle/state machine، execution algorithms، reconciliation، paper/live isolation، risk checks، kill switch، idempotency و order deduplication.

Candidates: NautilusTrader، LEAN، QuickFIX/QuickFIX-J، ccxt و broker SDKها.

**قانون:** چند trading engine به‌صورت همزمان runtime authority نیستند. benchmark و contract test تعیین می‌کند کدام implementation در هر boundary صاحب اجراست.

## 6. Domain 04 — AI / LLM / Agent Runtime

LLM abstraction، model routing، agent runtime، tool calling، structured output، planning، memory، MCP، local/cloud/fallback، model selection، token/cost management.

Candidates: LangGraph، Haystack، LlamaIndex، DSPy، PydanticAI، Microsoft Agent Framework/AutoGen، Semantic Kernel، CrewAI، Google ADK، Agno، OpenAI Agents SDK و MCP ecosystem.

**Elyrava باید framework-neutral باشد:** `Agent`, `Tool`, `Model`, `Memory`, `ResearchTask`, `Policy` contracts؛ framework فقط adapter/runtime است.

## 7. Domain 05 — Research Intelligence / Deep Research

Question → planning → decomposition → search planning → source selection → retrieval → evidence → verification → contradiction analysis → synthesis → citation validation → confidence → answer.

CFIP نباید «chatbot + RAG» تلقی شود. Research result باید dataset، query plan، source set، evidence IDs، timestamps، citation spans، contradictions و confidence را حفظ کند.

Candidates: LangGraph، Haystack، LlamaIndex، DSPy، Open Deep Research، STORM، Perplexica، Open WebUI و browser-agent ecosystems.

## 8. Domain 06 — Search & Retrieval

Lexical/BM25، dense، sparse، hybrid، vector، semantic، reranking/LTR، query expansion، facets، temporal/geo retrieval و search analytics.

Candidates: Vespa، OpenSearch، Elasticsearch، Qdrant، Weaviate، Milvus، pgvector، Typesense، Meilisearch، Tantivy، LanceDB، FAISS.

Vespa یا هر گزینه دیگر default نیست؛ benchmark باید recall، nDCG، latency، update cost، memory و operational complexity را تعیین کند.

## 9. Domain 07 — Web Acquisition

Discovery، crawl، scrape، browser automation، JS rendering، extraction، anti-bot handling، URL canonicalization، dedup، RSS/news/sitemap/archive، scheduling، politeness و source monitoring.

Candidates: Playwright، Selenium، Scrapy، Browser-use، Firecrawl، Crawl4AI، trafilatura، newspaper4k، readability، BeautifulSoup و httpx.

External content untrusted است؛ acquisition layer نباید اجازه دهد document/tool متن دلخواه را به policy یا authorization تبدیل کند.

## 10. Domain 08 — Document Intelligence

PDF/HTML/DOCX/XLSX/PPTX، OCR، tables، charts، layout، headers، footnotes، references، financial statements، papers، scans و multilingual.

Candidates: Docling، MinerU، Unstructured، Marker، PyMuPDF، PaddleOCR، Tesseract، Surya، Camelot و Tabula.

Output باید normalized document model با page/section/table/cell/span provenance باشد؛ parser implementation قابل تعویض است.

## 11. Domain 09 — Knowledge Graph & Memory

Entity، claim، evidence، temporal graph، semantic/episodic/long-term memory، entity resolution، ontology، graph reasoning و GraphRAG.

Candidates: Cognee، Semantica، VeritasGraph، Neo4j، Kuzu، Apache AGE، Memgraph، NetworkX.

Dedicated graph DB فقط وقتی وارد baseline می‌شود که benchmark ثابت کند Postgres + search + graph layer کافی نیست.

## 12. Domain 10 — Evidence / Provenance / Trust

**Evidence Contract جزو CFIP Core IP است.**

هر evidence باید source identity، authority، retrieval time، event/publication time، content hash، citation span، claim relation، support/contradiction، freshness، confidence و lineage داشته باشد.

حداقل مدل:

`Source → Artifact → EvidenceSpan → Claim → Relation → Decision`

Evidence قابل بازتولید باید بتواند نشان دهد «چه چیزی، از کجا، چه زمانی، با چه نسخه‌ای» مبنای یک conclusion بوده است.

## 13. Domain 11 — Machine Learning

Classical/deep ML، forecasting، classification/regression، clustering، anomaly/regime، embeddings، representation learning، RL، online/continual learning، fine-tuning/LoRA و synthetic data.

Candidates: PyTorch، scikit-learn، XGBoost، LightGBM، CatBoost، Hugging Face، PyTorch Forecasting، Darts، Nixtla، Ray و JAX.

## 14. Domain 12 — MLOps / LLMOps

Experiment tracking، model registry، dataset registry، feature store، deployment، monitoring، drift، lineage، evaluation و promotion.

Candidates: MLflow، Feast، DVC، Kubeflow، Optuna، Langfuse، Phoenix و ابزارهای evaluation.

Promotion فقط پس از gates: quality، regression، security، cost، drift، calibration و rollback readiness.

## 15. Domain 13 — Data Platform

Baseline: PostgreSQL + ClickHouse + Redis + Object Storage + DuckDB + Arrow/Parquet.

Polars/DataFusion می‌توانند برای analytical pipelines اضافه شوند. Vector/time-series اختصاصی فقط با evidence.

Ownership برای هر entity:

`owner → schema → writers → readers → retention → revision → deletion → audit`

## 16. Domain 14 — Streaming & Event Infrastructure

NATS JetStream baseline. Kafka، Redpanda، Pulsar و Redis Streams گزینه‌های benchmark هستند.

Event infrastructure با workflow یکی نیست. Business events باید schema/version داشته باشند؛ delivery semantics، idempotency، ordering، retry و DLQ مشخص باشد.

## 17. Domain 15 — Workflow / Distributed Execution

Candidates: Temporal، Prefect، Dagster، Airflow، Celery، Dramatiq، Arq، Hatchet.

همه با هم deploy نمی‌شوند. workflow class تعیین می‌کند کدام engine مناسب است. Long-running durable orchestration و ephemeral task execution نباید بی‌دلیل در یک abstraction مخلوط شوند.

## 18. Domain 16 — Evaluation / Intelligence QA

Metrics: retrieval recall/precision/MRR/nDCG، citation precision/recall، groundedness، faithfulness، contradiction، freshness، latency، token cost، calibration و financial outcome.

Candidates: Ragas، DeepEval، TruLens، Arize Phoenix، Langfuse، promptfoo، OpenAI Evals و Braintrust-like systems.

Golden datasets باید versioned و representative باشند؛ score بدون dataset provenance معتبر نیست.

## 19. Domain 17 — Observability

OpenTelemetry، Prometheus، Grafana، Loki، Tempo/Jaeger، OpenObserve، Langfuse/Phoenix و profiling.

سه سیگنال پایه: metrics + logs + traces. علاوه بر آن باید cost، model tokens، tool latency، research depth، evidence failures و business SLOها قابل مشاهده باشند.

## 20. Domain 18 — Security / Identity / Governance

OIDC/OAuth، RBAC/ABAC، secrets، supply chain، SBOM، runtime isolation، prompt-injection defense و audit.

Candidates: Keycloak، ZITADEL، Authentik، OpenFGA، OPA، Casbin، Vault، Infisical، SOPS/age، Trivy، Semgrep، Bandit، CodeQL، Gitleaks، Syft و Grype.

Authorization decision باید خارج از LLM و agent policy قرار گیرد. OpenFGA/OPA/Casbin implementation choice است، نه domain contract.

## 21. Domain 19 — Autonomous Elyrava / Self-Development

Repository indexing، code search، AST/code graph، issue analysis، debugging، patch generation، sandbox، test generation، benchmark، regression، research، experimentation، proposal، promotion و rollback.

Candidates: OpenHands، SWE-agent، Aider، Continue، Cline، OpenCode و Roo Code ecosystem.

Elyrava هرگز بدون policy gate، sandbox، least privilege، tests، diff review، evidence و rollback به production mutation دسترسی ندارد.

## 22. Domain 20 — Frontend / Terminal / Visualization

Next.js 16 + React + TypeScript + Tailwind + TradingView Lightweight Charts baseline. Canvas/WebGL فقط در نقاطی که benchmark توجیه کند.

UX باید chart-first، keyboard-first و responsive باشد: chart full-screen، tools در rail/bottom bar/drawer/modal/menu؛ نه dashboardهای طولانی و scrolling pages.

پشتیبانی: drawing، overlays، indicators، alerts، realtime، command palette، accessibility، PWA، SEO، i18n، RTL/LTR.

## 23. Domain 21 — Realtime

Market، signal، research، agent و notification events؛ NATS→WebSocket/SSE bridge؛ state synchronization؛ reconnection؛ backpressure؛ deduplication و ordering.

Realtime event نباید business truth را جایگزین storage durable کند.

## 24. Domain 22 — Payments / Subscription

Identity → plan → entitlement → checkout → payment intent → address/confirmation → verify → settle → subscription → activation → expiry → renewal/refund → reconciliation → audit.

Crypto candidates: BTCPay Server، Bitcoin/Lightning ecosystem و gateway/wallet infrastructure. Payment provider implementation نباید plan semantics را صاحب شود.

Free/Pro و limits باید configuration-driven باشند؛ هیچ price/limit/entitlement user-facing نباید hardcode شود.

## 25. Domain 23 — Testing / Reliability

pytest، Hypothesis، Schemathesis، Playwright، k6، Locust، mutation، contract/property/chaos/security/load/data/agent/RAG/financial simulation tests.

برای financial logic باید deterministic fixtures، invariant tests، PIT tests، replay tests، fill/slippage tests و numerical tolerance policy وجود داشته باشد.

## 26. Domain 24 — DevOps / Infrastructure

Docker/Compose برای local؛ Kubernetes/Helm برای scale در صورت نیاز؛ GitHub Actions؛ ArgoCD؛ Terraform/Pulumi/Ansible؛ backups، DR، secrets، service discovery، health، autoscaling، CDN و object storage.

Production deployment profile باید از constrained developer profile جدا باشد تا سخت‌افزار 8GB RAM مانع توسعه نشود.

## 27. Domain 25 — Developer Platform

Python 3.14، uv، Ruff، mypy یا pyright، pre-commit، OpenAPI، AsyncAPI، JSON Schema، Pydantic، SQLAlchemy 2، Alembic، codegen، CLI و architecture validation.

Dependency policy: stable releases، pinned/locked reproducibility، SBOM، vulnerability scanning، license inventory و periodic update windows.

## 28. Domain 26 — Financial Intelligence

Fundamental، macro، central-bank، news، sentiment، event impact، cross-asset، correlation، regimes، narrative، consensus، disagreement، analogues، scenarios، causal reasoning و forecast aggregation.

Financial intelligence باید evidence-aware باشد و uncertainty را صریح بیان کند.

## 29. Domain 27 — Decision Intelligence

Signal/evidence fusion، probabilistic reasoning، confidence/uncertainty، Bayesian inference، scenarios، counterfactuals، causal inference، decision policy و risk-adjusted decisioning.

**Research Decision Model جزو Core IP است.** تصمیم نهایی باید inputs، constraints، alternatives، uncertainty، policy و outcome measurement را ثبت کند.

## 30. Domain 28 — Governance of Intelligence

Dataset/model/prompt/agent governance، tool permissions، approval queue، experiments، promotion gates، audit، provenance، rollback و HITL.

AI proposal می‌تواند mature شود، اما promotion به runtime controlled است. هر promotion باید evidence package و rollback plan داشته باشد.

## 31. Domain 29 — Research Dataset / Knowledge Lifecycle

Discovery → ingestion → normalization → dedup → labeling → versioning → provenance → quality scoring → golden/benchmark/evaluation/retrieval/calibration/outcome datasets.

Dataset identity باید immutable/versioned باشد. حذف یا correction باید lineage را حفظ کند.

## 32. Domain 30 — Globalization / Accessibility

Persian/English/Arabic و multilingual architecture؛ RTL/LTR؛ locale/timezone؛ number/date/currency formatting؛ multilingual OCR/embeddings/search؛ keyboard navigation؛ screen-reader semantics و contrast/accessibility.

Domain semantics نباید به یک locale وابسته باشد. Translation keys و terminology registry باید versioned باشند.

---

# Part III — قراردادهای canonical

## 33. Contract Catalog

حداقل contracts:

- `InstrumentContract`
- `MarketDataProvider`
- `EconomicDataProvider`
- `NewsProvider`
- `FundamentalDataProvider`
- `HistoricalDataset`
- `PointInTimeSnapshot`
- `EvidenceContract`
- `ClaimContract`
- `SourceContract`
- `SearchProvider`
- `DocumentParser`
- `ResearchPlanner`
- `ResearchResult`
- `AgentContract`
- `ToolContract`
- `ModelProvider`
- `MemoryStore`
- `IndicatorContract`
- `StructureEngine`
- `FVGContract`
- `OrderBlockContract`
- `SignalContract`
- `ConsensusContract`
- `RiskEngine`
- `PositionSizingContract`
- `ExecutionBroker`
- `OrderLifecycle`
- `BacktestEngine`
- `ReplayEngine`
- `NotificationProvider`
- `PaymentProvider`
- `EntitlementPolicy`
- `DatasetRegistry`
- `ModelRegistry`
- `EvaluationRun`
- `PromotionProposal`
- `AuditEvent`

Contracts باید versioned، schema-first، idempotent در commandهای حساس و دارای compatibility policy باشند.

## 34. Evidence Contract

حداقل fields:

`evidence_id, source_id, artifact_id, locator, content_hash, retrieved_at, available_at, published_at?, span, claim_id?, relation, authority, freshness, confidence, extractor_version, provenance_chain`

Evidence باید بتواند به source artifact immutable یا content-addressed reference برگردد.

## 35. Signal Contract

حداقل:

`signal_id, instrument_id, timeframe, generated_at, data_snapshot_id, thesis, direction, trigger, invalidation, evidence_ids, confidence, model/engine versions, freshness, status`

## 36. Risk Contract

ورودی‌ها: equity، account، leverage، symbol specification، entry، stop، target، risk budget، fees، spread/slippage و broker constraints.

خروجی‌ها: allowed/not allowed، quantity، margin estimate، loss-at-stop، RR، constraints و reason codes.

Risk engine نباید به UI یا broker SDK وابسته باشد.

## 37. Research Result Contract

هر answer باید دارای `research_run_id`، question، plan، sources، evidence، claims، contradictions، synthesis، citations، confidence، freshness، limitations و timestamp باشد.

---

# Part IV — Data Truth، PIT و Replay

## 38. چهار زمان

- `event_time`: وقوع رویداد در بازار.
- `publication_time`: زمان انتشار منبع.
- `available_at`: زمانی که CFIP واقعاً می‌توانست از داده استفاده کند.
- `ingested_at`: زمان ورود به سیستم.

این زمان‌ها بدون دلیل یکی نمی‌شوند.

## 39. PIT Truth

برای decision time `t`:

`Visible(t) = {record | available_at <= t}`

Universe، خبر، fundamental، indicator، provider correction و dataset revision نباید با hindsight وارد historical decision شوند.

## 40. Replay Manifest

هر replay/backtest باید ثبت کند:

- dataset version
- provider/revision IDs
- universe definition
- engine versions
- feature versions
- execution assumptions
- spread/slippage/fees
- latency model
- deterministic ordering
- random seed
- output artifact hashes

---

# Part V — Trading Intelligence

## 41. Structure Canonicalization

Structure engine صاحب swing/trend/liquidity/shift/break semantics است. UI فقط renderer است.

### FVG lifecycle

`candidate → formed → qualified → active → mitigated/filled → invalidated → archived`

Formation، boundaries، ordering، MTF context و invalidation فقط یک semantic implementation دارند.

### Order Block

Origin، displacement، validation، mitigation و invalidation باید explicit باشند و با structure contract سازگار بمانند.

### MTF

Timeframe با duration واقعی bar تعریف می‌شود، نه صرفاً label. هر cross-timeframe relationship باید timestamp alignment داشته باشد.

## 42. Signal Fusion

`structure → features → independent analyses → signal candidates → evidence checks → consensus → decision`

Independence، weight، freshness، conflict و evidence quality باید در consensus ثبت شود. duplicate outputs نباید confidence مصنوعی بسازند.

## 43. Final Trade Answer

در صورت تولید تحلیل معاملاتی ساختاریافته:

- direction
- entry/trigger
- stop-loss
- target(s)
- invalidation
- risk budget
- position size
- leverage/margin constraint
- evidence/confidence
- timeframe
- data freshness
- generated timestamp

Execution authority از analytical recommendation جداست.

---

# Part VI — Research & Elyrava

## 44. Research Fabric

Pipeline canonical:

`Question → Planner → Decomposer → Query Planner → Acquisition → Retrieval → Evidence → Verification → Contradiction → Synthesis → Citation Validator → Confidence → Answer`

Parallelism مجاز است، اما result merge باید provenance و deterministic IDs را حفظ کند.

## 45. Elyrava Architecture

Elyrava یک intelligence layer cross-cutting است و domain owner نیست.

Subsystems:

1. Planner
2. Context Builder
3. Tool Router
4. Research Fabric
5. Evidence/Claim graph
6. Memory
7. Model Router
8. Evaluation
9. Policy Enforcement
10. Proposal Engine
11. Self-Diagnosis
12. Self-Improvement Controller

Agent action classes:

`READ → ANALYZE → PROPOSE → SANDBOX-EXECUTE → VERIFY → REQUEST-APPROVAL → PROMOTE`

برای production mutation، approval و gates اجباری‌اند مگر policy صریحاً action کم‌ریسک و reversible را auto-approve کرده باشد.

---

# Part VII — Autonomous Engineering

## 46. Self-Development Loop

`Observe → Diagnose → Research → Plan → Patch in Sandbox → Test → Benchmark → Security Scan → Review Evidence → Proposal → Approval → Canary/Promotion → Health Guard → Rollback if needed`

Sandbox باید network/filesystem/process permissions محدود داشته باشد. Secretها به agent داده نمی‌شوند مگر policy و scoped capability آن را مجاز کند.

## 47. Repository Intelligence

Indexing باید package/module/class/function/test/config/schema/route/event/dependency relationships را مدل کند. AST و code graph برای تغییرات cross-cutting از text grep قابل‌اعتمادترند.

هر patch autonomous باید diff، tests، affected components، risk classification، evidence و rollback strategy داشته باشد.

---

# Part VIII — Security, Identity, Privacy

## 48. Security Architecture

Defense in depth:

`Identity → Authentication → Authorization → Input Validation → Capability Policy → Sandbox → Audit → Detection → Recovery`

Threats: prompt injection، tool poisoning، SSRF، credential leakage، dependency compromise، malicious documents، data exfiltration، replay attacks، webhook spoofing، payment manipulation و privilege escalation.

## 49. Identity & Authorization

OIDC/OAuth برای identity؛ fine-grained authorization با OpenFGA/OPA/Casbin-like policy engine در adapter boundary.

Principles: least privilege، deny by default، tenant isolation، scoped tokens، short-lived credentials، auditable decisions.

## 50. Privacy / Residency / Retention

برای user data، research artifacts، raw market data، logs و payment data retention policy جدا تعریف می‌شود. Deletion request باید lineage و audit semantics را رعایت کند و در عین حال immutable financial/audit records را طبق policy حفظ کند.

---

# Part IX — API، Eventing و Frontend

## 51. API

FastAPI + Pydantic. API schemas از domain contracts مشتق می‌شوند ولی domain را به transport وابسته نمی‌کنند.

API rules: idempotency keys برای commands حساس، optimistic concurrency در state mutation، pagination، cursorهای stable، explicit error codes، correlation IDs، rate limits و audit metadata.

## 52. Eventing

NATS JetStream baseline. Events باید versioned schema، event_id، aggregate_id، occurred_at، producer، trace/correlation IDs و payload contract داشته باشند.

Outbox pattern برای business transactions. Consumers idempotent. Poison messages به DLQ/quarantine می‌روند.

## 53. Frontend Terminal

ساختار UX:

`Chart Canvas + Instrument/Timeframe Controls + Left Tool Rail + Bottom Context Bar + Right Intelligence Drawer + Modal/Command Surfaces`

بدون dashboard scrolling به‌عنوان interaction اصلی.

Realtime state باید reconcilable باشد. Chart renderer هیچ market/structure semantic را مالک نیست.

---

# Part X — Billing، Notifications، Journal

## 54. Billing

Entitlement از payment provider مستقل است. Payment event فقط input lifecycle است؛ activation توسط policy engine و durable subscription state انجام می‌شود.

Idempotency، webhook signature verification، settlement verification، reconciliation، refund، expiry و renewal اجباری‌اند.

## 55. Notifications

`Rule → Decision → Dedupe → Delivery Attempt → Provider → Receipt → Retry/Failure`

Channel adapters: in-app، Web Push، email، mobile push در آینده. User preference و quiet hours configuration-driven است.

## 56. Trading Journal & Outcome

Journal باید decision context، evidence، signal version، risk state، execution outcome، screenshots/artifacts، P&L، MAE/MFE، slippage و attribution را ذخیره کند.

Outcome loop:

`Prediction → Decision → Execution → Outcome → Attribution → Calibration → Learning`

---

# Part XI — OSS Adoption Matrix

## 57. Decision Ladder

`Use upstream → Adapter → Extension → Patch upstream → Fork → Build ourselves`

Fork آخرین گزینه است. Build خودمان فقط برای Core IP یا capabilityای که OSS پاسخ معتبر ندارد.

## 58. ارزیابی هر پروژه

برای هر candidate باید ثبت شود:

`functional_fit, maturity, activity, contributors, release_health, license, security, Python_3.14, performance, scalability, self_hosting, data_ownership, vendor_lock_in, API_quality, extensibility, ops_cost, community, docs, tests, migration_risk, benchmark, cfip_boundary, decision`

## 59. Shortlist مرجع

| حوزه | Candidates | نقش CFIP |
|---|---|---|
| Trading | NautilusTrader, LEAN, Qlib | adapter/benchmark |
| Data | OpenBB, yfinance, ccxt, fredapi, edgartools | provider adapters |
| Search | Vespa, OpenSearch, Qdrant, pgvector, Typesense | retrieval adapters |
| Web | Playwright, Scrapy, Crawl4AI, Firecrawl | acquisition adapters |
| Docs | Docling, MinerU, Unstructured, PyMuPDF, PaddleOCR | document adapters |
| Graph | Neo4j, Kuzu, AGE, Memgraph, Cognee | optional graph/memory adapters |
| Agents | LangGraph, Haystack, LlamaIndex, PydanticAI, ADK, Semantic Kernel | agent adapters |
| Research | Open Deep Research, STORM, Perplexica | research components/benchmarks |
| ML | PyTorch, sklearn, XGBoost, LightGBM, CatBoost, HF | ML substrate |
| MLOps | MLflow, Feast, DVC, Optuna | lifecycle adapters |
| Streaming | NATS JetStream, Kafka, Redpanda, Pulsar | event substrate benchmark |
| Workflow | Temporal, Prefect, Dagster, Airflow, Celery, Arq | workflow substrate |
| Eval | Ragas, DeepEval, Phoenix, Langfuse, promptfoo | eval/observability |
| Security | Keycloak, ZITADEL, OpenFGA, OPA, Vault, Trivy, Semgrep, CodeQL | adapters/tooling |
| Autonomy | OpenHands, SWE-agent, Aider, Continue, Cline, OpenCode | sandboxed engineering tools |
| Frontend | Next.js, React, Lightweight Charts | product UI |
| Payments | BTCPay Server, Bitcoin/Lightning tooling | payment adapter |

این shortlist «فهرست dependencyهای قطعی» نیست؛ هر مورد قبل از runtime adoption باید audit و benchmark شود.

---

# Part XII — Technology Baseline

## 60. Production Baseline

**Backend:** Python 3.14، FastAPI، Pydantic، SQLAlchemy 2، Alembic.  
**Events:** NATS JetStream.  
**Data:** PostgreSQL، ClickHouse، Redis، object storage، DuckDB، Arrow/Parquet.  
**Frontend:** Next.js 16، React، TypeScript، Tailwind، TradingView Lightweight Charts.  
**Tooling:** uv، Ruff، mypy/pyright، pytest، Hypothesis، Playwright، GitHub Actions، Docker/Compose.  
**Telemetry:** OpenTelemetry + metrics/logs/traces backend selected by deployment profile.

Technology substitutions require ADR + benchmark + migration plan.

---

# Part XIII — Reliability & Performance

## 61. Performance Budget

هر critical path باید latency budget داشته باشد: API، chart update، market ingestion، signal generation، research retrieval، citation validation، notification و payment webhook.

Measure:

`p50, p95, p99, throughput, concurrency, CPU, RAM, I/O, network, cache hit rate, query amplification`

N+1، synchronous blocking در async paths، unbounded queues و oversized payloadها ممنوع.

## 62. Resource Profiles

**Dev-Constrained:** مناسب 8GB RAM/CPU محدود؛ سرویس‌های optional با profiles؛ local models کوچک؛ bounded concurrency.  
**CI:** deterministic، isolated و reproducible.  
**Staging:** production-like.  
**Production:** scale-out و HA بر اساس SLO/capacity evidence.

---

# Part XIV — Testing & Release Gates

## 63. Whole-Repository Audit

هر release باید کل repository را بررسی کند، نه فقط feature جدید:

1. missing/zero-byte/marker-only files
2. imports and dependency resolution
3. runtime boot
4. Docker/Compose
5. migrations
6. API contracts
7. event contracts
8. unit/integration/e2e
9. security scans
10. performance/load
11. frontend accessibility/SEO/PWA/responsive
12. chart-first UX integrity
13. i18n/RTL/LTR
14. observability
15. backup/restore/DR
16. licensing/SBOM
17. docs/memory consistency
18. migration parity with CForex where applicable

## 64. Financial Test Gates

- deterministic indicator fixtures
- FVG lifecycle fixtures
- OB lifecycle fixtures
- MTF alignment
- PIT leakage tests
- replay determinism
- fill/slippage/fee invariants
- sizing/risk invariants
- broker constraint tests
- outcome attribution correctness

## 65. Agent/Research Gates

- prompt injection fixtures
- malicious document fixtures
- tool authorization tests
- citation correctness
- unsupported claim detection
- contradiction tests
- freshness tests
- retrieval metrics
- calibration
- token/cost budget
- sandbox escape tests

---

# Part XV — Governance

## 66. Promotion Gate

`Proposal → Static Validation → Unit/Contract → Integration → Security → Evaluation → Performance → Human/Policy Approval → Deployment → Health Guard → Auto-Rollback`

Promotion evidence باید immutable reference داشته باشد.

## 67. Configuration Governance

Provider, broker, model, limits, subscription, risk policy، feature flags و notification channels در configuration/policy layer تعریف می‌شوند. Secretها در secret manager هستند؛ config file محل secret نیست.

## 68. Audit

Audit event حداقل: actor، action، target، before/after reference، policy decision، timestamp، trace ID، reason، evidence و outcome.

Agent-generated changes نیز audit می‌شوند.

---

# Part XVI — Migration from CForex

## 69. Migration Principle

CForex source را عمیق می‌خوانیم و **رفتار، قرارداد و evidence** را استخراج می‌کنیم؛ فایل‌ها و ساختار قدیمی را کورکورانه کپی نمی‌کنیم.

Mapping:

`CForex artifact → capability → canonical contract → CFIP implementation/adaptor → parity test → evidence`

## 70. Migration Classification

هر artifact یکی از این‌هاست:

- Preserve behavior
- Refactor into domain
- Replace with OSS adapter
- Reimplement as CFIP Core IP
- Retire
- Needs evidence

`cforex-platform` در این classification قرار ندارد و مسیر مهاجرت نیست.

## 71. Parity

برای هر capability منتقل‌شده:

`source fixture → CFIP contract → implementation → expected behavior → regression test`

Parity به معنی حفظ bug نیست؛ behavior مورد تأیید و intended semantics باید منتقل شود و bugها باید صریحاً بهبود یابند.

---

# Part XVII — Architecture Decision Records

## 72. ADR Rules

هر تصمیم مهم باید شامل:

`Context → Problem → Options → Evidence → Decision → Consequences → Revisit trigger`

نمونه تصمیم‌های baseline:

- CFIP معماری مستقل از cforex-platform است.
- PostgreSQL transactional authority است.
- ClickHouse analytical plane است.
- Redis cache/ephemeral است.
- NATS JetStream event baseline است.
- Evidence Contract Core IP است.
- FVG/OB semantic engine Core IP است.
- Elyrava framework-neutral است.
- dedicated graph DB benchmark-gated است.
- چند workflow/trading engine همزمان baseline نیست.

---

# Part XVIII — Deployment & Operations

## 73. Service Boundaries

Initial bounded services/capabilities باید تا حد امکان coarse-grained باشند؛ microservice extraction فقط وقتی ownership، scaling یا isolation دلیل دارد.

Logical components:

`web-terminal, api, market-ingestion, research, search, intelligence, risk, execution, notifications, billing, admin, workers, event-bus, databases, object-store, observability`

این نام‌ها به معنی الزاماً یک container/service برای هر مورد نیستند.

## 74. Health Model

هر runtime component:

- liveness
- readiness
- dependency health
- queue lag
- error rate
- saturation
- freshness
- version

Health guard قبل و بعد از promotion بررسی می‌شود.

## 75. Backup / DR

PostgreSQL backup + restore verification؛ ClickHouse recovery strategy؛ object-store versioning؛ event retention؛ configuration backup؛ secret recovery process.

تعریف SLO باید RPO/RTO را همراه خود داشته باشد.

---

# Part XIX — Licensing & Supply Chain

## 76. OSS License Gate

قبل از adoption ثبت شود:

`license, copyright obligations, notice requirements, source-availability obligations, network-use implications, dependencies, transitive licenses, commercial restrictions`

هر license assessment باید برای نسخه دقیق dependency انجام شود.

## 77. Supply Chain

SBOM با Syft؛ vulnerability scan با Trivy/Grype؛ secret scan با Gitleaks؛ static analysis با Semgrep/Bandit/CodeQL در profile مناسب.

Lockfile، hashes، provenance و reproducible build تا حد امکان فعال باشند.

---

# Part XX — Research Dataset & Knowledge Graph

## 78. Dataset Classes

1. raw acquisition
2. normalized source
3. evidence corpus
4. golden research
5. retrieval benchmark
6. citation benchmark
7. calibration
8. financial outcome
9. agent trajectory
10. regression/security fixtures

هر dataset version باید owner، schema، provenance، license، temporal coverage، quality metrics و intended use داشته باشد.

## 79. Knowledge Lifecycle

`Acquire → Normalize → Resolve Entities → Extract Claims → Link Evidence → Validate → Version → Index → Evaluate → Retire/Revise`

Temporal validity و contradiction first-class هستند.

---

# Part XXI — Global UX & Accessibility

## 80. Localization

Locale-aware formatting برای timezone، DST، currency، decimal separator، dates و financial units. Internal storage همیشه canonical است؛ display localization در presentation layer.

## 81. Accessibility

Keyboard-first، focus management، semantic labels، ARIA در صورت نیاز، screen-reader support، reduced motion، contrast و non-color-only status indicators.

---

# Part XXII — Final Reference Graph

## 82. Logical Graph

```text
                    ┌─────────────────────────────┐
                    │        CFIP EXPERIENCE      │
                    │ Terminal / Chart / Admin    │
                    └──────────────┬──────────────┘
                                   │
                         API / WS / Commands
                                   │
                    ┌──────────────▼──────────────┐
                    │       APPLICATION LAYER      │
                    │ use-cases / policies / auth │
                    └──────────────┬──────────────┘
                                   │
        ┌──────────────────────────┼─────────────────────────┐
        │                          │                         │
 ┌──────▼──────┐            ┌──────▼──────┐          ┌──────▼──────┐
 │ Market/Trade│            │ Research &  │          │ Billing/User│
 │ Domain      │            │ Elyrava     │          │ Domain      │
 └──────┬──────┘            └──────┬──────┘          └──────┬──────┘
        │                          │                         │
        └──────────────────────────┼─────────────────────────┘
                                   │
                         Canonical Contracts
                                   │
                    ┌──────────────▼──────────────┐
                    │      CAPABILITY FABRIC      │
                    │ search/data/ML/docs/events  │
                    │ workflow/graph/observability│
                    └──────────────┬──────────────┘
                                   │
                           Adapter Boundaries
                                   │
        ┌──────────────┬───────────┼───────────┬──────────────┐
        ▼              ▼           ▼           ▼              ▼
      OSS Search     OSS Data    OSS ML     OSS Agents     OSS Ops
        │              │           │           │              │
        └──────────────┴───────────┼───────────┴──────────────┘
                                   ▼
                    PostgreSQL / ClickHouse / Redis
                    NATS JetStream / Object Storage
```

---

# Part XXIII — Complete Capability Graph Rules

## 83. Dependency direction

Domain → ports/contracts → adapters. Never adapter → domain semantics.

UI → API/contracts. Never UI → database directly.

Agent → tools through policy. Never agent → unrestricted shell/network/secrets.

Research → evidence. Never answer → unsupported text.

Backtest → PIT dataset + canonical engines. Never backtest → current mutable provider state.

Billing → entitlement policy. Never provider webhook → direct arbitrary access grant.

## 84. One semantic authority

For each concept exactly one owner is declared:

`FVG, OB, Structure, Signal, Risk, Instrument, Evidence, Claim, Entitlement, OrderState, Outcome, ResearchRun`

Other layers consume the contract.

---

# Part XXIV — Implementation Roadmap

## 85. Phase A — Foundation

Repository standards، package boundaries، contracts، config، identity، database، migrations، NATS، observability، CI، security baseline.

## 86. Phase B — Market Truth

Instrument registry، provider adapters، normalization، quality، PIT storage، ClickHouse analytical model، replay manifest.

## 87. Phase C — Trading Intelligence

Canonical structure، FVG/OB، indicators، signals، consensus، risk، sizing، backtest/replay، journal/outcome.

## 88. Phase D — Research Fabric

Acquisition، document parsing، search، evidence contract، citation validation، research planner، contradiction engine.

## 89. Phase E — Elyrava

Model routing، agent runtime، memory، tools، evaluation، proposal queue، sandboxed self-development.

## 90. Phase F — Terminal & Realtime

Chart workstation، command palette، overlays، alerts، WS bridge، notification system، accessibility/i18n.

## 91. Phase G — Billing & Production

Entitlement، crypto payment lifecycle، reconciliation، DR، production deployment، SLOs، capacity tests، supply-chain gates.

## 92. Phase H — Controlled Autonomy

Autonomous diagnosis/research/patch proposals، benchmark، promotion gates، rollback و continuous improvement.

---

# Part XXV — Definition of Done

## 93. Capability DoD

یک capability فقط وقتی «تمام» است که:

- contract دارد؛
- owner مشخص دارد؛
- implementation یا adapter مشخص دارد؛
- test executable دارد؛
- provenance/evidence دارد؛
- error/edge cases پوشش داده شده؛
- observability دارد؛
- security review شده؛
- performance budget دارد؛
- documentation دارد؛
- rollback/recovery در صورت state mutation دارد؛
- dependency/license ثبت شده؛
- CI آن را اجرا می‌کند.

## 94. Release DoD

Release بدون whole-repo audit، migration verification، test، security، performance، accessibility، i18n، observability، docs consistency و rollback evidence کامل محسوب نمی‌شود.

---

# Part XXVI — Final Master Checklist

## Architecture

- [ ] Domain ownership unique
- [ ] Contracts versioned
- [ ] Ports/adapters clean
- [ ] No accidental framework coupling

## Data

- [ ] PIT correctness
- [ ] Revision lineage
- [ ] Dataset identity
- [ ] Retention/deletion

## Trading

- [ ] FVG lifecycle
- [ ] OB lifecycle
- [ ] MTF alignment
- [ ] Signal fusion
- [ ] Risk invariants
- [ ] Replay determinism

## Research

- [ ] Evidence contract
- [ ] Citation validation
- [ ] Contradiction detection
- [ ] Freshness
- [ ] Confidence/calibration

## AI/Elyrava

- [ ] Model abstraction
- [ ] Tool policy
- [ ] Sandbox
- [ ] Memory provenance
- [ ] Evaluation
- [ ] Promotion gate
- [ ] Rollback

## Security

- [ ] OIDC/OAuth
- [ ] Fine-grained authorization
- [ ] Secrets isolation
- [ ] SBOM
- [ ] Vulnerability scan
- [ ] Prompt injection tests
- [ ] Audit trail

## Product

- [ ] Chart-first UX
- [ ] Realtime
- [ ] Notifications
- [ ] Journal
- [ ] Free/Pro entitlement
- [ ] Crypto payment reconciliation
- [ ] i18n/RTL/LTR
- [ ] Accessibility

## Operations

- [ ] Docker local profile
- [ ] Production profile
- [ ] Backups
- [ ] Restore test
- [ ] RPO/RTO
- [ ] SLO/alerts
- [ ] Capacity evidence

## OSS

- [ ] Official source checked
- [ ] Version pinned
- [ ] License recorded
- [ ] Security status checked
- [ ] Python/runtime compatibility checked
- [ ] Benchmark completed where material
- [ ] Adapter boundary defined
- [ ] No unnecessary fork

---

# Appendix A — Canonical vocabulary

**CFIP:** CForex Intelligence Platform.  
**Elyrava:** نام canonical intelligence layer.  
**Core IP:** semantics/contracts/algorithms whose correctness and differentiation belong to CFIP.  
**Capability Fabric:** generic capability layer assembled from reusable implementations.  
**PIT:** point-in-time historical truth.  
**Evidence:** auditable source-backed support for a claim.  
**Decision:** structured output produced under evidence, uncertainty and policy constraints.  
**Promotion:** controlled movement of an artifact/change into a higher-trust runtime state.

# Appendix B — Non-goals

CFIP در baseline این‌ها نیست:

- یک Laravel/PHP/Filament application؛
- معماری `cforex-platform`؛
- یک chatbot ساده؛
- یک RAG demo؛
- یک collection بی‌قاعده از microservices؛
- مجموعه‌ای از OSS frameworks بدون ownership؛
- یک autonomous agent با دسترسی unrestricted؛
- یک backtest که hindsight leakage دارد.

# Appendix C — Canonical repository contract

`armanemp/CForex` = source study / behavioral reference.  
`armanemp/CFIP` = implementation destination.  
`armanemp/CFIP-BOOK` = canonical architecture/engineering book.  
`cforex-platform` = abandoned and excluded.

هر سند معماری دیگر باید یا به این کتاب ارجاع دهد یا به‌عنوان ADR/implementation evidence با آن سازگار باشد. در صورت تعارض، جدیدترین ADR مصوب همراه با evidence اجرایی مرجع تصمیم است.

# Appendix D — Research protocol

برای هر OSS candidate:

1. official repository/docs را پیدا کن؛
2. release/current compatibility را بررسی کن؛
3. license و dependency graph را ثبت کن؛
4. activity، tests، security و maintenance را بررسی کن؛
5. performance/scalability را در صورت material بودن benchmark کن؛
6. integration boundary را تعریف کن؛
7. تصمیم را در matrix ثبت کن؛
8. قبل از runtime adoption evidence را archive کن.

این کتاب «فهرست مشهورترین پروژه‌ها» نیست؛ یک **decision system برای انتخاب و ترکیب capabilityها** است.

# Appendix E — Final architectural statement

CFIP باید یک سیستم منسجم باشد که از **market truth و research evidence** شروع می‌کند، آن‌ها را به **canonical domain intelligence** تبدیل می‌کند، از طریق **decision/risk models** به خروجی قابل‌تفسیر می‌رسد، نتیجه را در **journal/outcome** اندازه‌گیری می‌کند و از feedback برای **calibration و controlled improvement** استفاده می‌کند.

OSS سرعت و leverage می‌دهد؛ اما **semantic truth، evidence contract، decision model، FVG/OB intelligence، signal fusion، calibration، governance و Elyrava safety boundary مالکیت CFIP باقی می‌مانند.**

**پایان کتاب مرجع CFIP — 2026-09-16**
