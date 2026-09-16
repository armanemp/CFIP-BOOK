# CFIP — OSS Integration Master Matrix

**نسخه:** 2026-09-16  
**وضعیت:** Living execution matrix  
**مقصد:** `armanemp/CFIP`  
**مرجع معماری:** `CFIP-COMPLETE-BOOK.md`  
**منبع رفتاری:** `armanemp/CForex`  
**هوش پلتفرم:** Elyrava

> این سند رجیستری اجرایی OSS است؛ فهرست نام پروژه‌ها به‌تنهایی adoption محسوب نمی‌شود. هر مورد باید از discovery تا benchmark و rollback gate عبور کند.

## 1. قانون اجرایی

`Capability → Contract → Port → Candidate(s) → License/Provenance → Security → Compatibility → Benchmark → Test → Observability → Rollback → Decision → Evidence`

تصمیم‌های مجاز:

- **BUILD** — CFIP باید خودش پیاده‌سازی کند؛ معمولاً semantic/domain/governance IP.
- **INTEGRATE** — upstream به‌عنوان dependency/service استفاده می‌شود.
- **ADAPT** — upstream پشت CFIP port/adapter قرار می‌گیرد.
- **EXTEND** — extension رسمی بدون شکستن upstream boundary.
- **PATCH** — فقط با ضرورت اثبات‌شده و ADR.
- **FORK** — آخرین راه؛ مالکیت و merge burden مستند شود.
- **BENCHMARK** — برای مقایسه، بدون adoption.
- **REFERENCE** — ایده/الگو/fixture فقط.
- **REJECT** — evidence یا fit یا license/security/ops مانع است.

### وضعیت شواهد

`UNVERIFIED → DISCOVERED → IDENTIFIED → LICENSE-CHECKED → SECURITY-CHECKED → COMPATIBILITY-CHECKED → BENCHMARKED → TESTED → APPROVED → ADOPTED`

`ADOPTED` فقط با commit/ADR/evidence date معتبر است.

---

## 2. ستون‌های اجباری هر رکورد

| ستون | الزام |
|---|---|
| Domain | دامنه CFIP |
| Capability | قابلیت دقیق |
| CFIP Contract | قرارداد/semantic authority |
| Decision | BUILD/INTEGRATE/ADAPT/... |
| Candidate | پروژه OSS |
| Boundary | محل اتصال |
| License | license و compatibility |
| Runtime | Python/Node/Rust/Go و نسخه‌ها |
| PIT | سازگاری با point-in-time/replay |
| Security | threat/advisory/sandbox |
| Benchmark | معیار و نتیجه |
| Tests | test/CI evidence |
| Ops | deployment/resource burden |
| Rollback | مسیر برگشت |
| Evidence | لینک/commit/release/date |
| Status | lifecycle |
| Next action | قدم بعدی |

اگر یکی از ستون‌های critical خالی باشد، رکورد `ADOPTED` نیست.

---

# 3. Master Matrix

## A. Market Data, Instrument & Market Truth

| Capability | Decision | Candidate(s) | CFIP ownership / gate |
|---|---|---|---|
| Provider-neutral market-data port | BUILD | — | canonical contract؛ provider-neutral |
| FX spot/CFD/crypto adapters | ADAPT | OpenBB, ccxt, provider SDKs | normalize symbol/venue/time/quality |
| Economic/macro data | ADAPT | OpenBB, fredapi, Nasdaq Data Link tooling | publication/available_at/PIT |
| News/event feeds | ADAPT | OpenBB + provider adapters | source/evidence/freshness |
| Instrument master | BUILD | — | canonical instrument identity؛ no provider semantics |
| Corporate/reference metadata | ADAPT | OpenBB, edgartools/Arelle where relevant | provenance + revision |
| Tick/trade/order-book ingestion | ADAPT/BUILD | NautilusTrader, venue SDKs | canonical event schema + sequence |
| Data quality | BUILD | Great Expectations/Deequ class as reference | CFIP rules, quarantine, lineage |
| Provider reconciliation | BUILD | provider adapters | cross-source conflict + authoritative source policy |

## B. Historical Truth / PIT / Revision / Replay

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Four timestamps | BUILD | — | event/publication/available/ingested immutable semantics |
| Revision history | BUILD | — | no silent overwrite |
| PIT query engine | BUILD | PostgreSQL/ClickHouse/DuckDB substrate | `available_at <= t` |
| Dataset snapshot | BUILD | DVC/Parquet/object storage reference | content hash + manifest |
| Deterministic replay | BUILD | NautilusTrader/LEAN reference | ordering/clock/seed/fees/slippage |
| Replay manifest | BUILD | — | engine/data/feature/config identity |
| Historical parity | BUILD | CForex fixtures | CForex→CFIP parity evidence |

## C. Time-Series & Analytical Storage

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Transactional truth | INTEGRATE | PostgreSQL | schema/migration/constraints |
| Analytical truth | INTEGRATE | ClickHouse | query/partition/retention benchmark |
| Cache | INTEGRATE | Redis/Valkey | never source of truth |
| Research analytics | INTEGRATE | DuckDB | bounded local/research workload |
| Columnar interchange | INTEGRATE | Apache Arrow/Parquet | schema + metadata |
| Fast dataframe compute | ADAPT | Polars | benchmark vs pandas/Arrow |
| Query execution research | BENCHMARK | DataFusion | only if measured benefit |
| Alternative TS DB | BENCHMARK | QuestDB/TimescaleDB | no parallel baseline without evidence |

## D. Technical Analysis & Quant Substrate

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Primitive indicators | ADAPT/INTEGRATE | TA-Lib, NumPy/SciPy | deterministic/versioned outputs |
| Dataframe indicators | BENCHMARK | vectorbt, pandas-ta ecosystem | API/performance/licensing |
| Vectorized research | ADAPT | vectorbt | research-only boundary unless proven |
| Statistical models | INTEGRATE | statsmodels, SciPy | reproducibility |
| Forecasting | BENCHMARK/ADAPT | StatsForecast, MLForecast, NeuralForecast, Darts | temporal evaluation |
| Factor research | REFERENCE/ADAPT | Qlib | PIT/leakage audit |

## E. Market Structure / FVG / OB / MTF

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| FVG lifecycle | BUILD | — | canonical CFIP semantics |
| Order Block lifecycle | BUILD | — | canonical CFIP semantics |
| Liquidity/sweep semantics | BUILD | — | explicit event evidence |
| Market structure | BUILD | — | deterministic/versioned engine |
| MTF aggregation | BUILD | — | real duration + source timeframe evidence |
| Pattern fixtures | REFERENCE | TA/quant projects | never semantic authority |
| Structure benchmark | BENCHMARK | selected research libs | precision/recall against fixtures |

## F. Signals, Consensus & Decision Intelligence

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Signal contract | BUILD | — | hypothesis/action candidate only |
| Signal fusion | BUILD | NumPy/SciPy/sklearn substrate | weights/conflicts/freshness |
| Consensus | BUILD | statistical substrate | independence/conflict/evidence |
| Confidence/calibration | BUILD/ADAPT | sklearn, PyMC, SHAP | calibration + drift |
| Scenario engine | BUILD | PyMC/NumPyro/Pyro/DoWhy/EconML reference | uncertainty + provenance |
| Final trade answer | BUILD | — | CFIP authority; no OSS authority |
| Execution authorization | BUILD | — | separate from analysis |

## G. Risk, Portfolio & Position Sizing

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Risk contract | BUILD | — | account/venue-aware |
| Position sizing | BUILD | numerical substrate | equity/leverage/margin/SL/TP |
| Margin/leverage constraints | BUILD | broker adapters | venue-specific rules isolated |
| Portfolio optimization | ADAPT/REFERENCE | Qlib, SciPy, PyPortfolioOpt-class tooling | transaction costs + constraints |
| Risk analytics | ADAPT | NumPy/SciPy/statsmodels | deterministic tests |
| Kill switch / risk governor | BUILD | — | policy outside model |

## H. Backtest / Replay / Execution Simulation

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Event-driven backtest | ADAPT/BENCHMARK | NautilusTrader, LEAN, Backtrader, AAT | PIT + fill parity |
| Vectorized backtest | ADAPT/BENCHMARK | vectorbt, backtesting.py | cost/slippage correctness |
| Execution simulation | ADAPT | NautilusTrader/LEAN | order lifecycle + fees |
| Walk-forward | BUILD/ADAPT | Qlib/vectorbt references | temporal isolation |
| Paper trading | ADAPT | NautilusTrader/LEAN/Freqtrade reference | live/paper separation |
| Live execution | ADAPT | NautilusTrader/LEAN/broker SDKs | capital safety gate |
| Replay viewer | BUILD | chart UI | event sequence + deterministic clock |

## I. Outcome / Journal / Attribution / Drift

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Trade journal | BUILD | — | domain-owned |
| Signal outcome | BUILD | — | immutable outcome event |
| Attribution | BUILD | stats/ML substrate | signal→decision→execution→outcome lineage |
| Calibration | BUILD/ADAPT | sklearn/Evidently | temporal calibration |
| Drift | ADAPT/BUILD | Evidently/whylogs-class reference | market-regime awareness |
| Strategy/model scorecard | BUILD | MLflow metrics substrate | no simplistic leaderboard authority |

## J. Search / Retrieval / RAG

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Search port | BUILD | — | provider-neutral |
| Lexical search | ADAPT | OpenSearch/Elasticsearch/Tantivy/Quickwit | relevance + ops |
| Vector search | ADAPT | pgvector/Qdrant/Weaviate/Milvus/LanceDB/FAISS | recall/latency/resource |
| Hybrid retrieval | ADAPT/BUILD | Vespa/OpenSearch + vector stores | benchmark |
| Reranking | ADAPT | model ecosystem | relevance + latency |
| Temporal filters | BUILD | search backend | PIT/freshness semantics |
| Citation retrieval | BUILD | backend substrate | evidence span identity |
| Search evaluation | BUILD | Ragas/DeepEval/BEIR-class references | recall/MRR/nDCG/citation |

## K. Research Intelligence / Web / Documents

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Research planner | BUILD | LangGraph/PydanticAI/etc as runtime | CFIP task contract |
| Web acquisition | ADAPT | Playwright, Scrapy, Crawl4AI, httpx | SSRF/egress/rate limits |
| Browser agent | BENCHMARK/ADAPT | Browser Use, Playwright ecosystem | untrusted content isolation |
| Content extraction | ADAPT | trafilatura, readability, BeautifulSoup | reproducibility |
| PDF parsing | ADAPT | Docling, MinerU, PyMuPDF, Marker | page/block/span fidelity |
| OCR | ADAPT | PaddleOCR, Tesseract, Surya | multilingual accuracy |
| Tables | ADAPT | Camelot, Tabula | cell-level evidence |
| Office docs | ADAPT | python-docx, openpyxl, python-pptx | provenance |
| Research synthesis | BUILD | LLM substrate | evidence/citation/contradiction |
| Contradiction detection | BUILD/ADAPT | NLI/LLM ecosystem | evidence-linked result |

## L. Evidence / Provenance / Knowledge Graph

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Evidence model | BUILD | — | CFIP Core IP |
| Claim model | BUILD | — | source/span/time/hash |
| Provenance interchange | ADAPT | W3C PROV/OpenLineage | mapping only |
| Artifact lineage | ADAPT | DVC/MLflow/OpenLineage | hash/version |
| Knowledge graph | BENCHMARK/ADAPT | Neo4j, Kuzu, AGE, Memgraph, NetworkX, Cognee | workload benchmark |
| Graph RAG | BENCHMARK | LightRAG/GraphRAG ecosystem | evidence quality |
| Memory model | BUILD | graph/vector substrate | semantic authority |

## M. LLM / Agent Runtime

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Agent contract | BUILD | — | model-independent |
| Workflow/state graph | ADAPT | LangGraph | state/checkpoint/replay |
| Typed agent runtime | BENCHMARK/ADAPT | PydanticAI | contract fit |
| RAG orchestration | BENCHMARK/ADAPT | Haystack, LlamaIndex | boundary fit |
| Prompt/program optimization | BENCHMARK | DSPy | evaluation first |
| Multi-agent | BENCHMARK | AutoGen/Microsoft Agent Framework, CrewAI, Agno | no novelty-only adoption |
| Model routing | BUILD/ADAPT | LiteLLM | policy/cost boundary |
| Local inference | ADAPT | Ollama, llama.cpp | hardware/resource gate |
| High-throughput inference | ADAPT | vLLM | production GPU evidence |
| MCP integration | ADAPT | MCP SDKs | tool permission/policy gate |

## N. Elyrava Autonomous Intelligence

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Elyrava identity | BUILD | — | canonical platform intelligence |
| Research loop | BUILD | agent runtime substrate | evidence-first |
| Self-diagnosis | BUILD | observability + evaluation | no autonomous authority |
| Proposal generation | BUILD | agent/coding substrate | approval queue |
| Sandbox coding | ADAPT | OpenHands, SWE-agent, Aider, Roo Code, Cline, OpenCode | isolation + resource limits |
| AST/code analysis | ADAPT | tree-sitter, ast-grep | deterministic tooling |
| Auto-promotion | BUILD | CI/eval substrate | low-risk policy only |
| Rollback | BUILD | Git/OCI/deployment substrate | tested reversal |

## O. ML / RL / Model Lifecycle

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Classical ML | INTEGRATE | scikit-learn, XGBoost, LightGBM, CatBoost | reproducibility |
| Deep learning | INTEGRATE | PyTorch | model/data lineage |
| RL | BENCHMARK/ADAPT | FinRL, FinRL-Trading/FinRL-X, Stable-Baselines3, Ray RLlib | market realism + cost |
| Quant ML platform | BENCHMARK/ADAPT | Qlib | PIT/leakage/maintenance |
| Feature store | BENCHMARK/ADAPT | Feast | only if required |
| Experiment tracking | ADAPT | MLflow | artifact/metric lineage |
| Dataset versioning | ADAPT | DVC | snapshot provenance |
| Hyperparameter optimization | ADAPT | Optuna | reproducibility |
| Model explainability | ADAPT | SHAP | no causal overclaim |

## P. Evaluation / Intelligence QA

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Unit/property testing | INTEGRATE | pytest, Hypothesis | baseline |
| API contract testing | INTEGRATE | Schemathesis | OpenAPI correctness |
| Browser E2E | INTEGRATE | Playwright | terminal flows |
| Load testing | INTEGRATE | k6, Locust | SLO/capacity |
| RAG evaluation | ADAPT | Ragas, DeepEval, TruLens | evidence-linked metrics |
| LLM tracing/eval | ADAPT | Langfuse, Phoenix, Opik | privacy + cost |
| Prompt regression | BENCHMARK/ADAPT | promptfoo | golden datasets |
| Financial simulation | BUILD | — | domain truth |
| Replay/parity tests | BUILD | CForex fixtures + CFIP engines | historical behavior |

## Q. Observability / Reliability

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Traces | INTEGRATE | OpenTelemetry | semantic conventions |
| Metrics | INTEGRATE | Prometheus | SLOs |
| Dashboards | INTEGRATE | Grafana | operator UX |
| Logs | ADAPT | Loki | structured/auditable |
| Traces backend | BENCHMARK/ADAPT | Tempo, Jaeger, OpenObserve | resource/ops |
| Profiling | ADAPT | py-spy, Scalene | low overhead |
| GenAI telemetry | ADAPT | OTel GenAI + Langfuse/Phoenix/Opik | privacy/cost |
| Reliability state | BUILD | — | domain/service health semantics |

## R. Eventing / Streaming / Workflow

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Event bus | INTEGRATE | NATS JetStream | baseline |
| Alternative event bus | BENCHMARK | Kafka, Redpanda, Pulsar, RabbitMQ | no parallel baseline |
| Event schema | BUILD | AsyncAPI/JSON Schema/protobuf tooling | version/compatibility |
| Durable outbox | BUILD | PostgreSQL + application | before fan-out |
| Workflow engine | BENCHMARK/ADAPT | Temporal, Prefect, Dagster, Airflow, Hatchet | need-driven |
| Lightweight jobs | ADAPT | Celery, Dramatiq, Arq | only where workflow engine is overkill |
| Replay/DLQ | BUILD | event substrate | deterministic recovery |

## S. Identity / Authorization / Secrets

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| OIDC/OAuth | ADAPT | Google OIDC + Keycloak/ZITADEL/Authentik if needed | identity boundary |
| Authorization | ADAPT | OpenFGA/OPA/Casbin | policy external to agent |
| Secrets | ADAPT | Vault/Infisical/SOPS/age | secret isolation |
| Supply-chain scan | INTEGRATE | Trivy, Semgrep, Bandit, CodeQL, pip-audit, OSV | CI gate |
| SBOM | INTEGRATE | Syft/Grype ecosystem | artifact provenance |
| Secret leak scan | INTEGRATE | Gitleaks | pre-commit/CI |

## T. Frontend / Terminal / Visualization

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Terminal shell | BUILD | — | CFIP product identity |
| Chart | INTEGRATE | TradingView Lightweight Charts | chart-first UX |
| State/query | ADAPT | TanStack Query + Zustand/Redux Toolkit | complexity budget |
| Realtime client | BUILD/ADAPT | WebSocket/SSE + RxJS where useful | sequence/reconnect |
| E2E/a11y | INTEGRATE | Playwright, axe-core | keyboard/RTL/LTR |
| Component docs | BENCHMARK/ADAPT | Storybook | only if useful |
| PWA | BUILD | Next.js platform | offline/install behavior |
| Visualization extensions | BENCHMARK | Grafana ecosystem | terminal remains canonical |

## U. Realtime & Notifications

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Snapshot+delta stream | BUILD | NATS/WebSocket substrate | sequence + reconnect |
| Signal notifications | BUILD | provider-neutral notification port | dedup/idempotency |
| Email | ADAPT | SMTP/provider SDKs | delivery evidence |
| Push | ADAPT | Web Push/provider ecosystem | permission lifecycle |
| Webhook | BUILD | HTTP client/subsystem | signature/retry |
| Alert rules | BUILD | — | domain semantics |

## V. Payments / Subscription / Entitlement

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Crypto payment gateway | ADAPT | BTCPay Server | verification/settlement evidence |
| Lightning | ADAPT | Lightning ecosystem | settlement/reconciliation |
| Payment intent | BUILD | — | PostgreSQL truth |
| Subscription | BUILD | — | state machine |
| Entitlement | BUILD | — | authorization boundary |
| Reconciliation | BUILD | gateway/provider adapters | idempotent audit |
| Expiry/renewal | BUILD | — | deterministic scheduler/workflow |

## W. Admin / Provider / Broker Operations

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Provider registry | BUILD | — | admin-owned config |
| Broker account config | BUILD | broker adapters | secret isolation |
| Adapter health | BUILD | OTel substrate | evidence |
| Proposal queue | BUILD | — | approval/archive |
| Admin audit | BUILD | — | immutable event trail |
| Runtime feature flags | BUILD | — | no hardcoded user-facing values |

## X. Security / Supply Chain / Agent Safety

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| App security | BUILD + ADAPT | OWASP ASVS guidance | threat model |
| Agent safety | BUILD + ADAPT | OWASP Agentic AI, NIST AI RMF | policy/governor |
| Code scanning | INTEGRATE | CodeQL/Semgrep/Bandit | CI |
| Dependency vulnerabilities | INTEGRATE | Trivy/pip-audit/OSV | release gate |
| SBOM | INTEGRATE | Syft/Grype | artifact gate |
| Signing | BENCHMARK/ADAPT | Sigstore/cosign | supply-chain policy |
| Sandbox | BUILD + ADAPT | containers/Firecracker-class reference | escape/egress tests |
| Prompt injection defense | BUILD | — | content/instruction separation |

## Y. Data Governance / Privacy / Residency

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Data classification | BUILD | — | policy |
| Tenant isolation | BUILD | PostgreSQL/RLS + service policy | tests |
| Retention/deletion | BUILD | — | audit + legal policy |
| Residency | BUILD | deployment topology | evidence |
| Consent/PII boundaries | BUILD | — | privacy tests |
| Lineage | ADAPT | OpenLineage/DVC/MLflow | provenance |

## Z. DevOps / CI/CD / Release / Infrastructure

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Containers | INTEGRATE | Docker/Compose | boot/reproducibility |
| CI | INTEGRATE | GitHub Actions | full gates |
| Dependency update | ADAPT | Renovate/Dependabot | controlled upgrades |
| IaC | BENCHMARK/ADOPT later | Terraform/Pulumi | only when deployment complexity demands |
| Kubernetes | BENCHMARK/ADOPT later | Kubernetes/Helm/Argo CD | capacity/ops evidence |
| Local low-resource profile | BUILD | Compose | 8GB-friendly development target |
| Backup/DR | BUILD | PostgreSQL/object storage tooling | restore test |

## AA. Developer Platform / API Contracts

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Python runtime | INTEGRATE | Python 3.14 | supported wheels/deps |
| Package manager | INTEGRATE | uv | lock/reproducibility |
| API | INTEGRATE | FastAPI/Pydantic | OpenAPI |
| ORM/migrations | INTEGRATE | SQLAlchemy 2/Alembic | migration tests |
| Lint/format | INTEGRATE | Ruff | CI |
| Type checking | INTEGRATE | mypy/pyright | strictness policy |
| Schema | INTEGRATE | JSON Schema/OpenAPI/AsyncAPI | compatibility |
| Serialization | BENCHMARK | protobuf/Buf | only where justified |

## AB. Financial Intelligence / Macro / Narrative

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| Macro event ontology | BUILD | — | CFIP semantics |
| Fundamental intelligence | BUILD + ADAPT | OpenBB/provider adapters | evidence/PIT |
| Sentiment | ADAPT | Transformers/model ecosystem | source/time provenance |
| Cross-asset relationships | BUILD | NumPy/SciPy/Polars | deterministic |
| Regime detection | BUILD/ADAPT | sklearn/PyTorch/statsmodels | temporal stability |
| Narrative graph | BUILD | graph substrate | evidence links |
| Scenario mapping | BUILD | PyMC/NumPyro/DoWhy/EconML references | uncertainty |

## AC. Globalization / Accessibility

| Capability | Decision | Candidate(s) | Gate |
|---|---|---|---|
| i18n | INTEGRATE | Intl/FormatJS, next-intl | locale correctness |
| ICU/CLDR | INTEGRATE | ICU/CLDR | formatting semantics |
| Python locale | ADAPT | Babel | server-side formatting |
| RTL/LTR | BUILD | Next.js/Tailwind | visual + interaction tests |
| Accessibility | INTEGRATE | axe-core/Playwright | WCAG-oriented evidence |
| Multilingual OCR | ADAPT | PaddleOCR/Surya/Tesseract | language benchmark |

---

# 4. Candidate Decision Register

این رجیستر باید در هر release refresh شود. وضعیت اولیه عمدی است و تا زمانی که evidence واقعی جمع نشده `ADOPTED` نیست.

| Candidate | Intended role | Initial decision | Critical checks |
|---|---|---|---|
| NautilusTrader | trading/replay/execution benchmark/adaptation | BENCHMARK | license, PIT, Python 3.14, parity, live safety |
| QuantConnect LEAN | trading/backtest reference | BENCHMARK | license, boundary, data model, parity |
| vectorbt | vectorized research | BENCHMARK/ADAPT | research-only correctness, performance |
| Qlib | quant research/ML | BENCHMARK/ADAPT | PIT, leakage, Python compatibility, ops |
| FinRL | RL research | REFERENCE/BENCHMARK | production fit, data realism |
| FinRL-Trading / FinRL-X | AI-native trading research | BENCHMARK | current API/license/PIT/ops |
| OpenBB | financial data/research adapters | ADAPT candidate | provider licenses, freshness, API stability |
| OpenSearch | search | BENCHMARK | hybrid retrieval, ops, license |
| Qdrant | vector search | BENCHMARK | recall, latency, RAM, persistence |
| pgvector | vector search | BENCHMARK | workload vs dedicated vector DB |
| Vespa | hybrid search | BENCHMARK | relevance/ops complexity |
| Docling | document parsing | ADAPT candidate | PDF/table/span fidelity |
| Playwright | web acquisition/E2E | INTEGRATE candidate | SSRF/egress for acquisition; CI stability |
| LangGraph | agent orchestration | BENCHMARK/ADAPT | checkpoint/replay/policy boundary |
| PydanticAI | typed agent runtime | BENCHMARK | contract fit, maturity |
| LiteLLM | model routing | BENCHMARK/ADAPT | provider abstraction, secrets, cost |
| vLLM | high-throughput inference | ADAPT candidate | GPU/resource requirement |
| Ollama | local development inference | ADAPT candidate | local-only/dev profile |
| MLflow | experiment/model lifecycle | ADAPT candidate | artifact store, lineage, ops |
| DVC | dataset versioning | ADAPT candidate | PIT/snapshot workflow |
| OpenTelemetry | telemetry | INTEGRATE | semantic conventions + sampling |
| Prometheus/Grafana | metrics/ops | INTEGRATE | SLO/capacity |
| Keycloak/ZITADEL/Authentik | identity | BENCHMARK | only if native identity is insufficient |
| OpenFGA/OPA/Casbin | authorization/policy | BENCHMARK | policy model + operational burden |
| Trivy/CodeQL/Semgrep/Bandit | security | INTEGRATE | CI runtime + coverage |
| OpenHands/SWE-agent/Aider/Roo Code/Cline/OpenCode | coding autonomy | BENCHMARK | sandbox, egress, regression, approval |
| BTCPay Server | crypto payment gateway | ADAPT candidate | settlement/reconciliation |
| TradingView Lightweight Charts | chart | INTEGRATE | terminal UX/performance |

---

# 5. No-OSS / CFIP-Native Zone

این موارد عمداً به‌عنوان «پروژه آماده برای کپی» انتخاب نمی‌شوند:

1. FVG/OB/MTF canonical semantics.
2. CFIP Evidence/Claim/Decision graph semantics.
3. Signal fusion + consensus + final trade answer.
4. Financial decision contract and risk authority.
5. PIT/revision/replay truth semantics.
6. Entitlement/payment state machine.
7. Elyrava governance, policy, proposal queue and promotion authority.
8. CFIP capability registry and evidence lifecycle.
9. CForex parity mapping and migration truth.
10. Cross-domain audit/release gates.

OSS may provide substrate; CFIP remains semantic authority.

---

# 6. Adoption Gate — mandatory checklist

Before `ADOPTED`:

- [ ] exact upstream repository identified
- [ ] license and transitive-license compatibility verified
- [ ] release/version pinned
- [ ] Python/runtime compatibility verified
- [ ] security advisories reviewed
- [ ] dependency/SBOM scan completed
- [ ] architecture boundary defined
- [ ] CFIP port/adapter defined
- [ ] PIT/replay implications reviewed
- [ ] benchmark dataset and method defined
- [ ] correctness tests exist
- [ ] integration/contract tests exist
- [ ] observability hooks exist
- [ ] resource profile measured
- [ ] operational burden accepted
- [ ] failure modes documented
- [ ] rollback path tested
- [ ] evidence date recorded
- [ ] ADR/decision recorded
- [ ] release notes updated

No checkbox shortcut: missing evidence means non-adopted.

---

# 7. Anti-Cycle Execution Rule

برای جلوگیری از دور خود چرخیدن:

1. هر iteration فقط **یک capability slice** را target می‌کند.
2. ابتدا existing evidence و current repo state خوانده می‌شود.
3. اگر contract موجود است، دوباره طراحی نمی‌شود؛ فقط gap ثبت می‌شود.
4. اگر candidate قبلاً benchmark شده، دوباره benchmark نمی‌شود مگر نسخه/شرایط تغییر کرده باشد.
5. هر تغییر باید artifact قابل اجرا یا evidence جدید تولید کند.
6. discovery و implementation بی‌نهایت ادامه نمی‌یابد؛ برای هر domain یک decision checkpoint وجود دارد.
7. بعد از checkpoint، candidateهای بدون ارزش حذف/منجمد می‌شوند.
8. هیچ پروژه‌ای فقط به دلیل محبوبیت، stars یا README وارد baseline نمی‌شود.
9. `cforex-platform` در هیچ decision path قرار نمی‌گیرد.
10. پایان هر iteration: `what changed / evidence / remaining / next slice`.

---

# 8. Progress Accounting

پیشرفت CFIP بر اساس capability weighted evidence محاسبه می‌شود، نه تعداد فایل.

`Progress = verified capability points / total planned capability points`

هر capability حداقل این امتیازها را دارد:

- 0 — unmapped
- 1 — mapped
- 2 — contracted
- 3 — implemented
- 4 — verified
- 5 — parity-verified
- 6 — production-ready

OSS discovery به‌تنهایی امتیاز production نمی‌دهد.

### Release report minimum

- overall capability stage
- D1–D11 stage
- capabilities completed this iteration
- capabilities blocked
- new evidence
- tests added/passed
- OSS decisions changed
- security findings
- performance findings
- documentation delta
- exact next slice

---

# 9. Immediate Execution Order

1. Freeze this matrix as the OSS decision registry.
2. Re-read `CFIP-COMPLETE-BOOK.md` and reconcile contradictions.
3. Audit `armanemp/CForex` and map real capabilities to this matrix.
4. Build the CFIP capability matrix and assign evidence states.
5. Define contracts/ports for the first implementation slice.
6. Build foundation/runtime/security skeleton.
7. Implement market truth + PIT + provider boundary.
8. Implement canonical structure engines.
9. Implement signals/consensus/risk.
10. Implement research/search/evidence.
11. Implement replay/backtest/outcomes.
12. Implement Elyrava governance and agent runtime.
13. Implement terminal/realtime/notifications.
14. Implement billing/admin/operations.
15. Run full release audit and refresh OSS evidence.

The order may change only when a dependency or blocker is proven and documented.

---

# 10. Source Refresh Policy

This document is not a timeless claim about GitHub. At every meaningful release:

- re-check upstream repository existence;
- inspect latest stable release;
- inspect license;
- inspect Python/runtime support;
- inspect maintenance/CI/security;
- inspect breaking changes;
- rerun relevant benchmark;
- update evidence date;
- record decision changes.

Current external research confirms, for example, that Qlib remains an AI-oriented quantitative investment platform and that FinRL distinguishes its original research framework from FinRL-X/FinRL-Trading; NautilusTrader exposes a production-oriented event-driven trading architecture. These are research inputs, not automatic CFIP adoption decisions. citeturn0search1turn0search0turn0search4

---

# 11. Canonical Principle

> **CFIP does not compete with OSS by rewriting commodity infrastructure. It competes through contracts, financial semantics, evidence, PIT correctness, governance, orchestration, explainability, calibration, and differentiated intelligence.**
