# فهرست جامع پروژه‌ها و منابع Open-Source برای CFIP

## وضعیت این سند

این سند inventory جامع لایه Open-Source و GitHub برای CFIP است. هدف آن جدا کردن سه مفهوم است:

1. **Confirmed historical candidate**: در اسناد/بحث‌های قابل بازیابی به‌عنوان پروژه مورد بررسی یا استفاده مطرح شده است.
2. **Architecture reference**: برای استخراج ایده، الگو، benchmark یا methodology بررسی می‌شود؛ ادغام مستقیم تعهد نشده است.
3. **Adoption candidate**: ممکن است پس از license/security/compatibility/performance review به dependency یا adapter تبدیل شود.

وجود نام یک پروژه در این فهرست به معنی تأیید dependency یا کپی کد آن نیست.

اصل CFIP این است که ابتدا capability و contract مستقل از vendor/project تعریف شود و سپس پروژه مناسب در پشت port/adapter قرار گیرد.

---

# 1. Market Data / Financial Data Access

| پروژه | نقش در CFIP | وضعیت | قاعده استفاده |
|---|---|---|---|
| OpenBB | unified financial-data/provider abstraction و research data access | Adoption candidate / Reference | فقط پشت Provider Port؛ provider-specific semantics وارد domain نشود |
| FinResearch-Agent | reproducible financial-data + research workflow | Reference | ایده‌های reproducibility، factor research و methodology |
| Open-Papertrade | market/research/paper-trading workflow | Reference | استخراج workflow و separation، نه وابستگی مستقیم |

OpenBB برای equity، options، crypto، forex، macro و fixed income provider integrations ارائه می‌کند؛ بنابراین برای Provider Adapter Layer منبع مهمی است، ولی CFIP باید canonical market-data contract خودش را نگه دارد.

---

# 2. Time-Series / Analytical Storage

| پروژه | نقش | وضعیت | قاعده |
|---|---|---|---|
| ClickHouse | analytical market/time-series plane | Core target technology | storage authority برای analytics طبق معماری CFIP |
| PostgreSQL | transactional/control plane | Core target technology | business state و policy |
| Redis | cache/ephemeral acceleration | Core target technology | هرگز business truth نیست |
| DuckDB | local/research analytics | Core target technology / bounded | research artifact و local analytical workloads |
| QuestDB | high-throughput time-series reference | Reference / benchmark candidate | قبل از جایگزینی یا adoption باید benchmark واقعی CFIP انجام شود |
| TimescaleDB | PostgreSQL time-series reference | Reference | برای مقایسه schema/query/retention و در صورت نیاز adapter |
| Apache Arrow | columnar interchange | Reference/utility | interchange بین analytical tools و artifact pipelines |
| Parquet | immutable/open analytical artifact format | Core format candidate | dataset/research/export/PIT artifacts |

QuestDB در landscape فعلی روی ingestion، out-of-order data، deduplication، time partitioning و Arrow/Parquet تأکید دارد و باید به‌عنوان benchmark/reference بررسی شود، نه اینکه صرفاً به دلیل benchmark عمومی جایگزین ClickHouse شود.

---

# 3. Backtesting / Replay / Execution Simulation

| پروژه | نقش | وضعیت | قاعده |
|---|---|---|---|
| vectorbt OSS | vectorized research/backtesting reference | Adoption candidate / Reference | فقط از طریق Backtest Port؛ PIT و execution semantics باید تحت کنترل CFIP باشد |
| Backtrader | event-driven backtesting reference | Reference | برای execution/event semantics و parity tests |
| Zipline Reloaded | event-driven research/backtesting reference | Reference | مقایسه event clock و portfolio accounting |
| QuantConnect LEAN | production-oriented algorithmic trading/backtest reference | Reference | execution/risk/data architecture و parity benchmark |
| NautilusTrader | event-driven trading/backtest architecture | Reference / adoption candidate | در صورت نیاز به execution/replay infrastructure؛ بررسی license و operational fit الزامی |
| FINSABER | reproducible backtesting methodology | Reference | dataset, execution timing, slippage, liquidity cap و artifact discipline |
| ML4T/backtest | cross-engine parity/conformance reference | Reference / benchmark | استفاده برای contract/parity testing، نه جایگزینی canonical CFIP engine |
| h5i-db | PIT/replay/versioned time-series research reference | Reference / experimental | ایده‌های PIT، versioned reads و agent-safe writes |

**قانون قطعی:** CFIP نباید چند semantic backtest engine موازی برای یک capability بسازد. یک canonical execution/replay contract باید وجود داشته باشد و adapterها فقط implementation detail باشند.

---

# 4. Technical Analysis / Indicators / Quant Research

| پروژه/فناوری | نقش | وضعیت |
|---|---|---|
| vectorbt | indicator/vectorized research reference | Reference / candidate |
| TA-Lib ecosystem | indicator implementation reference | Reference |
| pandas-ta ecosystem | indicator breadth/reference | Reference |
| Polars | high-performance dataframe/feature processing | Technology candidate |
| NumPy/SciPy | numerical primitives | Core supporting technologies |

برای FVG، Order Block، liquidity، structure، MTF و سایر semantics، پروژه خارجی نباید semantic authority باشد. این قابلیت‌ها باید در CFIP canonical engineهای versioned خودشان تعریف شوند.

---

# 5. Quantitative ML / Factor Research / RL

| پروژه | نقش | وضعیت | قاعده |
|---|---|---|---|
| FinRL | financial reinforcement learning | Reference / candidate |
| FinRL-X | AI-native modular quant infrastructure | Reference / candidate |
| Qlib | quantitative research / ML workflow | Reference |
| FinResearch-Agent | factor research + risk-aware reproducible workflow | Reference |
| MLflow | experiment/model lifecycle | Governance/tooling candidate |
| Stable-Baselines3 | RL algorithm implementation | Candidate behind ML port |
| Ray RLlib | distributed RL | Candidate for bounded training workloads |

RL/ML models are research components, not uncontrolled execution authorities. Training datasets, PIT rules, seeds, model versions and promotion evidence are mandatory.

---

# 6. LLM / Agentic Financial Intelligence

| پروژه | نقش | وضعیت | قاعده |
|---|---|---|---|
| TradingAgents | multi-agent financial analysis patterns | Reference |
| FinResearch-Agent | reproducible research agent workflow | Reference |
| Open-Papertrade | LLM behavioral coaching / research patterns | Reference |
| FinRL / FinRL-X | AI-native quantitative workflows | Reference |
| FinGPT ecosystem | finance-oriented open LLM research | Reference |

این پروژه‌ها منبع pattern هستند؛ Elyrava مالک orchestration/policy/evidence boundary است. هیچ agent خارجی نباید policy، authorization، audit یا safety controls را کنترل کند.

---

# 7. Search / RAG / Research Intelligence

| پروژه/فناوری | نقش | وضعیت |
|---|---|---|
| Alpha Search | quantitative research/search workflow reference | Reference |
| OpenBB | data discovery/provider research | Reference/candidate |
| FinResearch-Agent | research planning + evidence synthesis | Reference |
| h5i-db | agent-safe data access/PIT ideas | Reference |
| Elasticsearch/OpenSearch class systems | lexical/vector retrieval reference | Architecture candidate |
| pgvector | vector retrieval in PostgreSQL | Technology candidate |

Search output باید provenance، citation، freshness، source identity و confidence داشته باشد. محتوای خارجی untrusted است و قبل از tool use یا prompt construction باید isolation و validation داشته باشد.

---

# 8. Trading Terminal / Frontend / Chart Workstation

| پروژه | نقش | وضعیت | قاعده |
|---|---|---|---|
| OpenTerminalUI | terminal UX/workstation reference | Reference |
| OpenTerminal | lightweight terminal UX/charting reference | Reference |
| BB-Terminal | OpenBB + React + Lightweight Charts terminal reference | Reference |
| TradingView Lightweight Charts | primary chart rendering technology | Core target technology |
| Grafana | operational/observability dashboards | Supporting technology; not primary product UI |

CFIP باید chart-first terminal باشد، نه clone UI. Workspace، command palette، synchronized panels، replay، overlays، drawing tools و responsive behavior از landscape استخراج می‌شوند ولی product semantics و visual identity اختصاصی CFIP باقی می‌مانند.

---

# 9. Eventing / Streaming / Workflow

| فناوری/پروژه | نقش | وضعیت |
|---|---|---|
| NATS JetStream | durable event streaming | Core target technology |
| Kafka | streaming/reference benchmark | Reference |
| Redpanda | Kafka-compatible streaming reference | Reference |
| Temporal | durable workflow orchestration reference | Reference / candidate |
| Dagster | data/research orchestration reference | Reference |
| Prefect | workflow orchestration reference | Reference |

NATS JetStream در معماری فعلی CFIP primary event backbone است. جایگزینی آن بدون capacity/operational evidence مجاز نیست.

---

# 10. Observability / Reliability / Operations

| فناوری | نقش | وضعیت |
|---|---|---|
| OpenTelemetry | traces/metrics/log correlation | Core target technology |
| Prometheus | metrics reference/collector | Supporting candidate |
| Grafana | dashboards/alert visualization | Supporting candidate |
| Loki | log aggregation reference | Supporting candidate |
| Tempo/Jaeger | trace backend reference | Supporting candidate |
| OpenTelemetry GenAI semantic conventions | AI observability | Required governance/reference |

SLO/SLI، trace correlation، worker health، provider health، queue lag، replay latency و model/tool telemetry باید بخشی از release evidence باشند.

---

# 11. Security / Agent Safety / Governance

| استاندارد/پروژه | نقش | وضعیت |
|---|---|---|
| OWASP Agentic AI guidance | agent threat model | Required reference |
| OWASP ASVS | application security baseline | Required reference |
| NIST AI RMF | AI risk governance | Required reference |
| OpenTelemetry GenAI | AI observability | Required reference |
| Sigstore/cosign class tooling | artifact provenance/signing | Supply-chain candidate |
| Trivy class tooling | container/dependency scanning | CI security candidate |
|

Security controls باید مستقل از agent و business logic enforcement باشند.

---

# 12. Notification / Integration / External Providers

CFIP باید provider/broker/notification ports داشته باشد و پروژه‌های خارجی فقط adapter باشند. نمونه‌های landscape برای بررسی:

- broker/data adapters exposed by OpenBB ecosystem
- CCXT-class crypto exchange adapters
- broker adapters such as Interactive Brokers/Alpaca ecosystems
- webhook/email/push notification providers

این‌ها به معنی انتخاب vendor یا dependency قطعی نیستند؛ provider selection باید از Admin/Configuration و entitlement policy بیاید.

---

# 13. پروژه‌هایی که نباید وارد معماری مقصد شوند

### cforex-platform

**صریحاً خارج از scope است.** این پروژه مسیر قبلی و منسوخ است و نباید architecture، module layout، migration target یا dependency source باشد.

### پروژه‌های صرفاً UI clone

کد یا naming محصولاتی که صرفاً clone یک terminal تجاری هستند نباید به‌عنوان product identity CFIP وارد شوند.

### پروژه‌های بدون evidence کافی

یک repository صرفاً به دلیل GitHub بودن، star، benchmark تبلیغاتی یا README طولانی dependency قابل قبول نیست.

---

# 14. تصمیم Adoption

هر پروژه قبل از ورود به dependency یا source reuse باید این gate را عبور کند:

`Discover → License → Provenance → Security → Dependency audit → Architecture fit → API/contract fit → Performance benchmark → PIT/replay audit → Test/CI evidence → Operational burden → Cost → Rollback → Approval`

### طبقه‌بندی نهایی

- **Core technology**: جزء architecture رسمی CFIP است.
- **Adapter candidate**: فقط پشت port و adapter قابل استفاده است.
- **Research reference**: برای methodology/pattern/benchmark.
- **Experimental**: sandbox و بدون production authority.
- **Rejected**: ناسازگار با license/security/architecture/maintenance یا scope.

---

# 15. Research Cycle جاری — منابع صریح بررسی‌شده

- Open-Papertrade — https://github.com/Open-Papertrade/Open-Papertrade
- FINSABER — https://github.com/waylonli/FINSABER
- FinResearch-Agent — https://github.com/Caspian-Lin/FinResearch-Agent
- TradingAgents — https://github.com/SboTeaman/trading-agents
- Backtrader derivative reviewed — https://github.com/cloudQuant/backtrader
- FinRL — https://github.com/AI4Finance-Foundation/FinRL
- FinRL-Trading / FinRL-X — https://github.com/AI4Finance-Foundation/FinRL-Trading
- OpenTerminalUI — https://github.com/laanito/OpenTerminalUI
- OpenTerminal — https://github.com/ErTasselli/OpenTerminal
- BB-Terminal — https://github.com/vaughanf1/BB-Terminal
- Alpha Search — https://github.com/alpha-search/alpha-search
- h5i-db — https://github.com/Koukyosyumei/h5i-db
- ML4T/backtest — https://github.com/ml4t/backtest
- OpenBB — https://github.com/OpenBB-finance/OpenBB
- QuestDB — https://github.com/questdb/questdb
- QuestDB streaming analytics template — https://github.com/questdb/time-series-streaming-analytics-template
- Qlib — https://github.com/microsoft/qlib
- NautilusTrader — https://github.com/nautechsystems/nautilus_trader
- QuantConnect LEAN — https://github.com/QuantConnect/Lean
- Zipline Reloaded — https://github.com/stefan-jansen/zipline-reloaded
- Backtrader — https://github.com/mementum/backtrader
- vectorbt — https://github.com/polakowo/vectorbt
- Freqtrade — https://github.com/freqtrade/freqtrade

---

# 16. نکته مهم درباره «کامل بودن»

این inventory عمداً بین **آنچه قبلاً به‌عنوان candidate مطرح شده** و **آنچه در research جدید برای پوشش خلأهای معماری پیدا شده** تفکیک می‌کند. نباید پروژه‌ای را صرفاً برای پر کردن فهرست به‌عنوان «قبلاً قرار بود ادغام شود» ثبت کرد.

در نتیجه، از این نسخه به بعد هیچ پروژه Open-Source جدیدی نباید بدون ثبت در همین inventory وارد CFIP شود. هر adoption واقعی باید یک record شامل license، commit/tag، capability mapping، owner، adapter boundary، test evidence، security review و rollback plan داشته باشد.
