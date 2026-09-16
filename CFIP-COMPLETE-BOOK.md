# CFIP — کتاب جامع معماری، اکوسیستم OSS و نقشه اجرای مرجع

**نسخه:** 2026-09-16 | **وضعیت:** Canonical Living Book | **مقصد:** `armanemp/CFIP` | **منبع:** `armanemp/CForex` | **هوش:** Elyrava

> این کتاب برای جلوگیری از پراکندگی تصمیم‌ها نوشته شده است. هر پروژهٔ آماده فقط candidate است؛ ورود به runtime منوط به contract، license، security، compatibility، benchmark، observability و rollback است.

## 0. قانون اصلی

`CFIP Contract → Adapter → OSS Implementation → Evidence → Gate → Adoption`

CFIP مالک contract، domain semantics، Evidence، governance و intelligence متمایز است. OSS implementation عمومی را فراهم می‌کند. هیچ OSS نباید مستقیم domain را آلوده کند.

`cforex-platform` از معماری و مسیر مهاجرت حذف شده و نباید مبنای تصمیم باشد.

## 1. معماری

`Experience → Inbound → Application → Domain → Ports → Capability Fabric → OSS Adapters → Infrastructure`

Experience: Next.js/React/TypeScript، terminal chart-first، TradingView Lightweight Charts، keyboard-first، PWA، RTL/LTR.

Inbound: HTTP، WebSocket، event consumer، scheduler، internal command.

Application: use case، orchestration، transaction boundary، entitlement، policy، idempotency، audit.

Domain: Market، Instrument، TimeSeries، Structure، Indicator، Signal، Consensus، Risk، Execution، Research، Evidence، Journal، Outcome، Learning، Elyrava.

Ports: MarketDataProvider، EconomicDataProvider، NewsProvider، DocumentParser، SearchProvider، VectorStore، Broker، ExecutionEngine، ModelProvider، AgentRuntime، MemoryStore، WorkflowEngine، EventBus، ArtifactStore، IdentityProvider، PolicyEngine، NotificationProvider.

## 2. اصول غیرقابل مذاکره

1. Evidence قبل از ادعا.
2. Capability معیار پیشرفت است، نه LOC.
3. هر مفهوم semantic authority واحد دارد.
4. Point-in-Time برای research/backtest/ML اجباری است.
5. چهار زمان `event_time / publication_time / available_at / ingested_at` جدا هستند.
6. revision گذشته را silently overwrite نمی‌کند.
7. Redis source of truth نیست.
8. business event مهم ابتدا durable می‌شود.
9. policy و authorization بیرون model/agent است.
10. web/PDF/GitHub/news untrusted است.
11. baseline فقط stable release.
12. scale بدون benchmark/SLO/capacity/cost evidence پذیرفته نیست.
13. fork/build بدون ADR ممنوع.
14. destructive change باید reversible باشد.
15. high-impact decisions باید governed باشند.

## 3. چرخه‌ها

Capability: `MAPPED → CONTRACTED → IMPLEMENTED → VERIFIED → PARITY-VERIFIED → PRODUCTION-READY`

Evidence: `DISCOVERED → IDENTIFIED → EXTRACTED → VERIFIED → NORMALIZED → PROVEN → AUDITED`

OSS adoption: `USE UPSTREAM → ADAPTER → EXTENSION → PATCH → FORK → BUILD`

---

# 4. ماتریس جامع ۳۰ حوزه و پروژه‌های آماده

## 01 — Forex / Trading / Quant Core

**قابلیت:** market data، tick، OHLCV، order book، microstructure، TA، price action، market structure، liquidity، FVG، OB، supply/demand، S/R، MTF، patterns، indicators، signals، strategy، backtest، walk-forward، replay، paper/live، portfolio، sizing، leverage، margin، SL/TP، journal، attribution.

**پروژه‌ها:**
- NautilusTrader — event-driven trading/research/live.
- QuantConnect LEAN — backtest/live engine.
- Backtrader — event-driven backtesting/reference.
- backtesting.py — lightweight research.
- AAT — asynchronous algorithmic trading.
- RQAlpha — quant/backtest candidate; license/fit gate.
- Qlib — quant research/ML.
- vectorbt — vectorized research.
- Freqtrade — crypto trading reference.
- TA-Lib — technical indicators.

**CFIP BUILD:** FVG lifecycle، OB semantics، MTF evidence، signal fusion، consensus، confidence، final analysis، outcome attribution.

## 02 — Market & Financial Data

**پروژه‌ها:** OpenBB، yfinance، pandas-datareader، fredapi، ccxt، Nasdaq Data Link tooling، Alpha Vantage integrations، Financial Modeling Prep integrations، Polygon/Massive integrations، Databento tooling، sec-edgar-downloader، edgartools، Arelle، exchange-native SDKs.

**قاعده:** provider وارد domain model نمی‌شود. قراردادها provider-neutral هستند.

## 03 — Trading Engine & Execution

FIX، REST/WebSocket، order state machine، reconciliation، paper/live isolation، kill switch، idempotency.

**پروژه‌ها:** NautilusTrader، LEAN، QuickFIX، QuickFIX/J، ccxt، broker SDKs، IB ecosystem.

## 04 — AI / LLM / Agent Runtime

**پروژه‌ها:** LangGraph، Haystack، LlamaIndex، DSPy، PydanticAI، AutoGen/Microsoft Agent Framework، Semantic Kernel، CrewAI، Google ADK، Agno، OpenAI Agents SDK، MCP SDKs، LiteLLM، vLLM، Ollama، llama.cpp.

**CFIP:** framework-neutral Agent/Tool/Model/Memory/ResearchTask/Policy contracts.

## 05 — Research Intelligence / Deep Research

Canonical flow:
`Question → Planner → Decomposer → Search → Retrieval → Evidence → Verification → Contradiction → Synthesis → Citation Validation → Confidence → Answer`

**پروژه‌ها:** Open Deep Research implementations، STORM، Perplexica، Open WebUI، LightRAG، RAG-Anything، Agent-Reach، browser-agent ecosystem، LangGraph، Haystack، LlamaIndex.

Research result باید query plan، source set، evidence IDs، timestamps، citation spans، contradictions، confidence و reproducibility manifest داشته باشد.

## 06 — Search & Retrieval

BM25، dense/sparse، hybrid، vector، reranking، filters، temporal/geo، facets، LTR.

**پروژه‌ها:** Vespa، OpenSearch، Elasticsearch، Qdrant، Weaviate، Milvus، pgvector، Quickwit، LanceDB، FAISS، Typesense، Meilisearch، Tantivy.

Benchmark: recall@k، precision@k، MRR، nDCG، filter latency، update latency، RAM/index size.

## 07 — Web Acquisition

**پروژه‌ها:** Playwright، Selenium، Scrapy، Crawl4AI، Firecrawl، Browser Use، Scrapling، httpx، BeautifulSoup، trafilatura، newspaper4k، readability.

Security: SSRF، URL validation، egress policy، rate limits، canonicalization، dedup، sandbox و prompt-injection isolation.

## 08 — Document Intelligence

**پروژه‌ها:** Docling، MinerU، Unstructured، Marker، PyMuPDF، PaddleOCR، Tesseract، Surya، Camelot، Tabula، python-docx، openpyxl، python-pptx.

Canonical normalized model:
`Document → Page → Block → Section → Table → Cell → Span → CitationAnchor`

## 09 — Knowledge Graph & Memory

**پروژه‌ها:** Cognee، Neo4j، Kuzu، Apache AGE، Memgraph، NetworkX، LightRAG، GraphRAG ecosystem.

Graph DB فقط با benchmark وارد baseline می‌شود؛ Postgres + search ابتدا بررسی می‌شود.

## 10 — Evidence / Provenance / Trust

**CFIP Core IP.**

`Source → Artifact → EvidenceSpan → Claim → Relation → Decision`

Evidence: source identity، artifact identity، locator، retrieval time، event/publication/available time، content hash، parser version، citation span، support/contradiction، freshness، authority، confidence، lineage.

OSS support: W3C PROV، OpenLineage، MLflow، DVC، OpenTelemetry.

## 11 — Machine Learning

**پروژه‌ها:** PyTorch، scikit-learn، XGBoost، LightGBM، CatBoost، Hugging Face Transformers، Hugging Face Datasets، sktime، StatsForecast، MLForecast، NeuralForecast، Darts، PyTorch Forecasting، Ray، JAX، PyOD، SHAP.

Financial ML باید temporal split، leakage test، regime stability، calibration و transaction-cost-aware outcome داشته باشد.

## 12 — MLOps / LLMOps

**پروژه‌ها:** MLflow، Feast، DVC، Kubeflow، Optuna، Langfuse، Arize Phoenix، Opik، Evidently، Weights & Biases ecosystem.

Promotion: quality + regression + security + cost + drift + calibration + reproducibility + rollback.

## 13 — Data Platform

**Baseline:** PostgreSQL + ClickHouse + Redis/Valkey + Object Storage + DuckDB + Arrow/Parquet.

**پروژه‌ها:** Polars، DataFusion، LanceDB، MinIO/S3 ecosystem.

Ownership: owner، schema، writers، readers، retention، revision، deletion، audit.

## 14 — Streaming & Events

**Baseline:** NATS JetStream.

**پروژه‌ها:** NATS، Kafka، Redpanda، Pulsar، Redis Streams، RabbitMQ، Schema Registry ecosystem، AsyncAPI ecosystem.

Event باید schema/version، idempotency، ordering، retry، DLQ، retention و replay semantics داشته باشد.

## 15 — Workflow / Distributed Execution

**پروژه‌ها:** Temporal، Prefect، Dagster، Airflow، Celery، Dramatiq، Arq، Hatchet.

Workflow و event bus یک چیز نیستند. همهٔ این‌ها همزمان deploy نمی‌شوند.

## 16 — Evaluation / Intelligence QA

**پروژه‌ها:** Ragas، DeepEval، TruLens، Arize Phoenix، Langfuse، Opik، promptfoo، OpenAI Evals ecosystem، Braintrust ecosystem، pytest، Hypothesis، Schemathesis.

Metrics: retrieval، citation، groundedness، contradiction، freshness، latency، cost، calibration، financial outcome.

## 17 — Observability

**پروژه‌ها:** OpenTelemetry، Prometheus، Grafana، Loki، Tempo، Jaeger، OpenObserve، Langfuse، Phoenix، Opik، py-spy، Scalene.

Elyrava telemetry: research depth، evidence failures، tool latency، token/cost، citation validation، confidence، signal outcome، policy denial.

## 18 — Security / Identity / Governance

**Identity:** Keycloak، ZITADEL، Authentik.  
**Authorization:** OpenFGA، OPA، Casbin.  
**Secrets:** Vault، Infisical، SOPS، age.  
**Supply chain:** Trivy، Semgrep، Bandit، CodeQL، Gitleaks، Syft، Grype، pip-audit، OSV.

Model/agent هرگز authority برای authorization نیست.

## 19 — Autonomous Elyrava / Self-Development

**پروژه‌ها:** OpenHands، SWE-agent، Aider، Continue، Cline، OpenCode، Roo Code، tree-sitter، ast-grep، code-search ecosystems.

Pipeline:
`Observe → Diagnose → Propose → Sandbox → Test → Security Scan → Benchmark → Approval → Promote → Monitor → Rollback`

## 20 — Frontend / Terminal / Visualization

**Baseline:** Next.js 16 + React + TypeScript + Tailwind + TradingView Lightweight Charts.

**Supporting:** TanStack Query، Zustand/Redux Toolkit، RxJS، Playwright، Vitest، Storybook، axe-core.

UX: fullscreen chart، side rail، bottom bar، drawers/modals، command palette، keyboard-first، responsive، PWA، RTL/LTR.

## 21 — Realtime

`Market/Event → NATS → Consumer → Projection → WebSocket/SSE → Terminal`

Requirements: snapshot+delta، sequence، reconnect، backpressure، dedup، ordering، heartbeat، auth، tenant isolation.

## 22 — Payments / Subscription

`Checkout → Intent → Address/Invoice → Verify → Settle → Subscription → Entitlement → Activation → Renewal/Expiry → Reconciliation`

**OSS:** BTCPay Server، Bitcoin ecosystem، Lightning ecosystem، wallet/gateway SDKs.

Payment truth و entitlement در PostgreSQL/domain-owned؛ webhook idempotent و auditable.

## 23 — Testing / Reliability

pytest، Hypothesis، Schemathesis، Playwright، k6، Locust، mutation testing، contract/property/chaos/security tests، financial simulation، RAG/agent evaluation، data-quality tests.

Layers: `unit → contract → integration → component → E2E → load → security → replay/parity → financial outcome`.

## 24 — DevOps / Infrastructure

Docker/Compose، Kubernetes، Helm، GitHub Actions، Argo CD، Terraform، Pulumi، Ansible، S3/object storage، Renovate/Dependabot ecosystem.

Low-resource development: Compose + single-node services. Kubernetes فقط با نیاز عملیاتی.

## 25 — Developer Platform

**Baseline:** Python 3.14 + uv + Ruff + mypy/pyright + pre-commit + Pydantic + SQLAlchemy 2 + Alembic + FastAPI + OpenAPI + JSON Schema + AsyncAPI.

**Supporting:** protobuf، Buf، documentation/codegen tooling.

## 26 — Financial Intelligence

Fundamental، macro، central bank، news، sentiment، event impact، cross-asset، correlation، regimes، narrative، consensus، disagreement، analogue، scenario، causal، forecast aggregation.

OSS building blocks: OpenBB، pandas/Polars، SciPy، statsmodels، scikit-learn، PyTorch، XGBoost/LightGBM/CatBoost، Nixtla، Transformers، search ecosystem.

CFIP Core: financial ontology، event semantics، evidence weighting، disagreement، narrative graph، scenario/decision mapping.

## 27 — Decision Intelligence

Bayesian inference، uncertainty، scenarios، counterfactuals، causal inference، policy، risk-adjusted decisions، attribution.

**پروژه‌ها:** PyMC، NumPyro، Pyro، SciPy، statsmodels، DoWhy، EconML، SHAP.

## 28 — Governance of Intelligence

Dataset/model/prompt/agent/tool governance، approval queue، experiments، promotion، audit، provenance، rollback، HITL، policy-as-code.

OSS: MLflow، DVC، OpenFGA، OPA، OpenTelemetry، Langfuse/Phoenix/Opik، GitHub Actions، CodeQL، SBOM tooling.

## 29 — Research Dataset / Knowledge Lifecycle

`Discover → Ingest → Normalize → Deduplicate → Label → Version → Provenance → Quality → Evaluate → Publish/Archive`

OSS: DVC، Hugging Face Datasets، Arrow/Parquet، DuckDB، Polars، MLflow، OpenLineage، object storage.

Dataset identity: hash + schema + source manifest + time window + provider revisions + transformation versions.

PIT rule: `Visible(t) = records where available_at <= t`.

## 30 — Globalization / Accessibility

Persian/English/Arabic، RTL/LTR، locale، timezone، number/date/currency، multilingual embeddings، OCR، keyboard/accessibility.

OSS: ICU، CLDR، Babel، Intl/FormatJS، next-intl، axe-core، Playwright accessibility tooling، multilingual OCR/model ecosystem.

---

# 5. Decision Matrix: چه چیزی را می‌سازیم و چه چیزی را reuse می‌کنیم؟

| Capability | CFIP Core | OSS role |
|---|---|---|
| FVG/OB semantics | بله | reference/testing |
| Evidence Contract | بله | provenance helpers |
| Signal fusion | بله | numerical/ML substrate |
| Consensus | بله | statistical substrate |
| Final trade answer | بله | none as authority |
| Research decision model | بله | orchestration substrate |
| Trading engine | خیر، مگر gap اثبات شود | Nautilus/LEAN/etc |
| Search engine | خیر | Vespa/OpenSearch/Qdrant/etc |
| PDF parser | خیر | Docling/MinerU/etc |
| OCR | خیر | PaddleOCR/Tesseract/Surya |
| Agent runtime | contract بله، runtime خیر | LangGraph/PydanticAI/etc |
| Model serving | contract بله | vLLM/Ollama/llama.cpp |
| Workflow | contract بله | Temporal/Prefect/etc |
| Identity | contract بله | Keycloak/ZITADEL/etc |
| Policy engine | contract بله | OpenFGA/OPA/Casbin |
| ML framework | خیر | PyTorch/sklearn/etc |
| Observability | semantics/telemetry schema بله | OTel/Prometheus/etc |

---

# 6. Benchmark Gate

### Trading
Replay parity، throughput، p50/p95/p99، fill/slippage، memory، startup، live/paper/replay parity.

### Search
Recall/precision/MRR/nDCG، citation support، filters، update latency، RAM/index size.

### Documents
Text recall، table accuracy، layout، citation anchors، multilingual OCR، pages/minute، memory/page.

### Research
Evidence recall، citation precision، contradiction، freshness، source diversity، reproducibility، latency، token/tool cost.

### ML
Temporal validation، leakage، calibration، regime stability، drift، PnL after costs، drawdown/risk.

### Autonomy
Task success، regression، unsafe actions، sandbox escape، tests، patch quality، rollback.

---

# 7. Data Truth و Replay

چهار timestamp همیشه جداست: `event_time / publication_time / available_at / ingested_at`.

Revision باید provenance داشته باشد.

Replay identity:
`dataset_snapshot + provider_revision + universe + clock + ordering + feature_versions + engine_version + execution_assumptions + fees + spread + slippage + seed + output_manifest`.

Engine identity:
`engine_id + version + descriptor + implementation + inputs + parameters + output_schema + fixtures + tests`.

---

# 8. Trading Semantics

FVG:
`candidate → formed → qualified → active → mitigated/filled → invalidated → archived`

Order Block: origin + displacement + validation + mitigation + invalidation.

MTF: duration واقعی bar + evidence.

Indicator: deterministic/versioned feature.

Signal: hypothesis/action candidate.

Consensus: vote + weight + independence + conflict + freshness + confidence.

Final answer:
`direction + entry zone/trigger + SL + targets + invalidation + risk budget + position size + leverage constraint + confidence + evidence + timeframe + timestamp + freshness`.

Execution authority جداست.

---

# 9. Elyrava

Elyrava یک model نیست؛ governed intelligence layer است.

اجزا: Research Planner، Evidence Manager، Retrieval Orchestrator، Verification، Contradiction، Market Structure، Signal Fusion، Decision، Memory، Model Router، Tool Registry، Policy Engine، Outcome Learner، Calibration، Proposal Queue، Self-Diagnostics، Sandbox.

Self-improvement فقط:
`Research → Hypothesis → Dataset → Experiment → Evaluation → Proposal → Approval → Promotion → Monitoring → Rollback`

---

# 10. Security

External content همیشه untrusted. Content و instruction جدا. Tool permissions خارج model. URL allowlist/validation. SSRF protection. Sandbox. Secret isolation. Egress policy. Output validation. Immutable audit. Approval برای destructive/high-impact action.

هیچ PDF/web page نباید بتواند به‌تنهایی trade، payment یا authorization ایجاد کند.

---

# 11. Runtime Profiles

### Local / Low Resource
PostgreSQL، NATS، Redis/Valkey، ClickHouse محدود، DuckDB، Parquet، optional MinIO، Ollama/llama.cpp، API/worker محدود.

### Small Production
فقط failure/scale boundaries واقعی جدا شوند.

### Scale
Horizontal API، NATS cluster، ClickHouse cluster، object storage، dedicated search، GPU inference و workflow workers فقط پس از capacity evidence.

---

# 12. License / Supply Chain

قبل از adoption: LICENSE، transitive dependencies، advisories، artifact provenance، SBOM، self-hosting، egress، vendor lock-in، resource cost، rollback و evidence date بررسی شود.

وضعیت license/activity/Python 3.14 ثابت نیست و باید هر release refresh شود.

---

# 13. Definition of Done

یک OSS capability فقط زمانی ADOPTED است که capability، repo identity، license، runtime/Python compatibility، security، boundary، benchmark، resource profile، tests، observability، rollback و evidence date مشخص باشند.

---

# 14. نقشه اجرای نهایی

**Phase 0:** foundation/contracts/security.  
**Phase 1:** market truth/PIT/providers.  
**Phase 2:** structure/FVG/OB/MTF/signals/consensus/risk.  
**Phase 3:** web/doc/search/evidence/research.  
**Phase 4:** quant/replay/backtest/outcomes.  
**Phase 5:** Elyrava/agents/memory/policy/evaluation.  
**Phase 6:** datasets/ML/calibration/drift/governance.  
**Phase 7:** terminal/realtime/alerts/journal/i18n/a11y.  
**Phase 8:** crypto payments/entitlement/reconciliation/scale.

---

# 15. Release Gate

کل repo هر release audit می‌شود: missing/empty/marker-only files، imports/runtime، Docker/package/test، security، performance، N+1/index/cache/async، frontend chart-first/accessibility/SEO/PWA/responsive، FVG/OB/MTF regression، worker/logging، research evidence/citation/freshness، AI policy/sandbox، payment idempotency/reconciliation، replay/PIT/parity، docs/memory/ADR، OSS/license refresh و rollback.

---

# 16. فهرست نهایی OSS برای جلوگیری از فراموشی

**Trading:** NautilusTrader، LEAN، Backtrader، backtesting.py، AAT، RQAlpha، Qlib، vectorbt، Freqtrade، TA-Lib.  
**Data:** OpenBB، yfinance، pandas-datareader، fredapi، ccxt، Nasdaq Data Link، Alpha Vantage، FMP، Polygon/Massive، Databento، sec-edgar-downloader، edgartools، Arelle.  
**AI:** LangGraph، Haystack، LlamaIndex، DSPy، PydanticAI، AutoGen/Microsoft Agent Framework، Semantic Kernel، CrewAI، Google ADK، Agno، OpenAI Agents SDK، MCP، LiteLLM، vLLM، Ollama، llama.cpp.  
**Research:** Open Deep Research، STORM، Perplexica، Open WebUI، LightRAG، RAG-Anything، Agent-Reach.  
**Search:** Vespa، OpenSearch، Elasticsearch، Qdrant، Weaviate، Milvus، pgvector، Quickwit، LanceDB، FAISS، Typesense، Meilisearch، Tantivy.  
**Web:** Playwright، Selenium، Scrapy، Crawl4AI، Firecrawl، Browser Use، Scrapling، httpx، BeautifulSoup، trafilatura، newspaper4k، readability.  
**Docs:** Docling، MinerU، Unstructured، Marker، PyMuPDF، PaddleOCR، Tesseract، Surya، Camelot، Tabula، python-docx، openpyxl، python-pptx.  
**Graph:** Cognee، Neo4j، Kuzu، Apache AGE، Memgraph، NetworkX، LightRAG، GraphRAG.  
**ML:** PyTorch، scikit-learn، XGBoost، LightGBM، CatBoost، Transformers، Datasets، sktime، StatsForecast، MLForecast، NeuralForecast، Darts، PyTorch Forecasting، Ray، JAX، PyOD، SHAP.  
**MLOps/Eval:** MLflow، Feast، DVC، Kubeflow، Optuna، Ragas، DeepEval، TruLens، Phoenix، Langfuse، Opik، promptfoo، OpenAI Evals، Evidently.  
**Data:** PostgreSQL، ClickHouse، Redis/Valkey، DuckDB، Arrow، Parquet، Polars، DataFusion، MinIO/S3.  
**Events/Workflow:** NATS JetStream، Kafka، Redpanda، Pulsar، Redis Streams، RabbitMQ، Temporal، Prefect، Dagster، Airflow، Celery، Dramatiq، Arq، Hatchet.  
**Security:** Keycloak، ZITADEL، Authentik، OpenFGA، OPA، Casbin، Vault، Infisical، SOPS، age، Trivy، Semgrep، Bandit، CodeQL، Gitleaks، Syft، Grype، pip-audit، OSV.  
**Autonomy:** OpenHands، SWE-agent، Aider، Continue، Cline، OpenCode، Roo Code، tree-sitter، ast-grep.  
**Frontend:** Next.js، React، TypeScript، Tailwind، Lightweight Charts، TanStack Query، Zustand/Redux Toolkit، RxJS، Playwright، Vitest، Storybook، axe-core.  
**Decision:** PyMC، NumPyro، Pyro، SciPy، statsmodels، DoWhy، EconML، SHAP.  
**Payments:** BTCPay Server، Bitcoin، Lightning.  
**Globalization:** ICU، CLDR، Babel، Intl/FormatJS، next-intl، axe-core.

---

## وضعیت این کتاب

این سند **comprehensive candidate inventory و canonical architecture book** برای CFIP است؛ «همه پروژه‌های GitHub جهان» ادعا نمی‌شود. هر candidate باید در release audit با evidence روز از نظر license، maintenance، security، Python 3.14 و performance بازبینی شود. نام پروژه به‌تنهایی adoption را ثابت نمی‌کند.

**اصل نهایی:**

> **CFIP مالک contract، semantics، Evidence، governance و differentiated intelligence است؛ OSS implementation عمومی را فراهم می‌کند؛ Adapter مرز رسمی این دو است.**
