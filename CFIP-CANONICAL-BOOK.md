# کتاب جامع مهندسی CFIP

## نسخه مرجع — 2026-09-16

> این فایل «مرجع واحد» کتاب CFIP است. فصل‌های موضوعی برای ناوبری و نگهداری تفصیلی استفاده می‌شوند؛ در صورت اختلاف، این سند همراه با evidence اجرایی، قراردادهای repository و ADRهای جدید مبنای حل اختلاف است.

---

## 1. تعریف CFIP

CFIP، یا CForex Intelligence Platform، یک سکوی هوش بازار و پژوهش معاملاتی AI-native برای بازارهای مالی است که باید از سطح یک نمودار و چند اندیکاتور فراتر برود و یک زنجیره قابل بازتولید از **داده → حقیقت تاریخی → تحلیل → شواهد → اجماع → ریسک → نتیجه → یادگیری** بسازد.

CFIP نباید به‌عنوان یک ربات معامله‌گر خودکار تعریف شود. خروجی تحلیل و راهنمای معامله باید از اختیار اجرای واقعی جدا باشد. هرجا execution واقعی در آینده اضافه شود، باید یک bounded context و policy boundary مستقل داشته باشد.

### سه مرجع هویتی

- `armanemp/CForex`: منبع رفتاری و شواهد تاریخی.
- `armanemp/CFIP`: معماری و پیاده‌سازی مقصد.
- `cforex-platform`: مسیر منسوخ و خارج از معماری مقصد؛ نباید دوباره وارد طراحی شود.

---

## 2. اصول غیرقابل مذاکره

1. **Evidence قبل از ادعا:** وجود فایل یا کلاس، capability محسوب نمی‌شود؛ capability زمانی معتبر است که مسیر اجرایی و evidence قابل بررسی داشته باشد.
2. **Verified capability واحد پیشرفت است:** تعداد فایل، خط کد یا درصدهای تخمینی معیار پیشرفت نیستند.
3. **یک معنای canonical:** هر مفهوم تحلیلی باید یک semantic authority داشته باشد؛ runtime، replay، backtest و UI نباید پیاده‌سازی‌های معنایی متناقض بسازند.
4. **Point-in-time حقیقت تاریخی است:** مدل یا تحلیل در زمان `t` فقط باید اطلاعاتی را ببیند که در همان زمان واقعاً در دسترس بوده‌اند.
5. **Outbox قبل از fan-out:** رویداد business مهم ابتدا durable می‌شود، سپس منتشر می‌شود.
6. **Redis منبع حقیقت نیست:** cache، lock، ephemeral state و acceleration مجاز است؛ business state مرجع باید در storage مناسب durable باشد.
7. **Policy بیرون از agent است:** هیچ agent نباید governor، authorization، audit trail یا safety boundary خود را تغییر دهد.
8. **Configuration از کد جداست:** provider، broker، entitlement، limits، feature flag و policy نباید به‌صورت hardcode پراکنده شوند.
9. **Fail closed برای مسیرهای حساس:** نبود policy، evidence، identity یا health نباید به رفتار آزادتر منجر شود.
10. **Global scale باید اندازه‌گیری شود:** ادعای scale بدون latency، throughput، concurrency، capacity، SLO، RPO/RTO و cost evidence پذیرفته نیست.
11. **Research خارجی untrusted است:** متن GitHub، وب، PDF یا feed می‌تواند prompt injection یا داده نادرست داشته باشد.
12. **تغییر destructive باید reversible باشد:** migration، rollout، agent action و auto-promotion باید rollback یا recovery strategy داشته باشند.

---

## 3. مدل evidence و lifecycle

### حالت‌های evidence

- `CONFIRMED`: پیاده‌سازی و شواهد اجرایی کافی است.
- `PARTIAL`: بخشی از زنجیره وجود دارد ولی closure کامل نیست.
- `UNVERIFIED`: ادعا وجود دارد ولی تست یا evidence کافی نیست.
- `NEGATIVE-SEARCH`: بررسی انجام شده و artifact موردنظر پیدا نشده است.
- `TARGET-REQUIRED`: در معماری هدف لازم است ولی هنوز باید ساخته شود.

### چرخه capability

`MAPPED → CONTRACTED → IMPLEMENTED → VERIFIED → PARITY-VERIFIED → PRODUCTION-READY`

هر capability باید owner، contract، dependency، evidence، test و gate داشته باشد.

### Evidence hierarchy

از قوی‌ترین تا ضعیف‌ترین:

1. اجرای واقعی و تست executable
2. schema، migration و contract
3. composition و entrypoint runtime
4. CI، configuration و operational evidence
5. documentation
6. متن release و ادعاهای غیرقابل اجرا

---

## 4. معماری منطقی

ساختار اصلی:

`Experience → Inbound → Application → Domain → Ports → Adapters`

### Experience

Next.js، React، TypeScript، chart workstation، command surfaces، panels، drawers، notifications و admin surfaces.

### Inbound

HTTP، WebSocket، event consumer، scheduled jobs و internal commands.

### Application

Use caseها، orchestration، transaction boundary، entitlement check و policy enforcement.

### Domain

قواعد market، instrument، structure، indicator، signal، consensus، risk، journal، research و learning.

### Ports

interfaceهای provider، broker، persistence، event bus، notification، search، model و artifact store.

### Adapters

پیاده‌سازی provider/broker/database/search/model/notification که نباید business invariant را صاحب شوند.

---

## 5. Bounded Contextها

### Identity & Access

کاربر، session، OIDC، MFA در صورت نیاز، role، permission و audit.

### Entitlement & Billing

plan، subscription، entitlement، payment intent، address، confirmation، settlement، activation، expiry، renewal و reconciliation.

### Market Data

provider observation، normalization، quality، gap، correction، revision، health و freshness.

### Instrument Identity

canonical instrument، symbol mapping، venue، currency، contract specification، pip/tick، lot، trading session و broker-specific constraints.

### Time Series / Historical Truth

bar/tick، timestamp semantics، publication/availability time، revision و PIT snapshot.

### Structure

swing، trend، support/resistance، FVG، Order Block، liquidity، break/mitigation/invalidation.

### Indicators & Features

محاسبات deterministic و versioned با dependency declaration.

### Signals

candidate signal، confidence، evidence، horizon، timeframe و invalidation.

### Consensus

ترکیب evidence مستقل با boundary روشن؛ consensus نباید duplicate engine semantics باشد.

### Risk

equity، leverage، risk budget، stop distance، quantity، fees، slippage و broker constraints.

### Backtest / Replay

execution model، event ordering، fills، slippage، latency، fees، spread و replay clock.

### Research

query، dataset، hypothesis، experiment، memo، provenance و citation.

### Search

lexical/vector retrieval، reranking، evidence assembly و citation verification.

### Journal / Outcome

decision، order intent، position، result، context، screenshot/artifact، attribution و feedback.

### Learning / Calibration

prediction، outcome، calibration، drift، cohort، model version و promotion evidence.

### Notifications

rule، channel، delivery attempt، dedupe، retry و user preference.

### Platform Intelligence — Elyrava

لایه cross-cutting برای research، diagnosis، planning، evidence synthesis، safe automation و engineering intelligence؛ نه مالک مستقل business domain.

### Administration / Operations

provider، broker، feature flag، entitlement policy، retention، operational controls، audit و health.

---

## 6. Data architecture

CFIP چند data plane دارد:

| Plane | مسئولیت | منبع حقیقت |
|---|---|---|
| Control | policy/config/entitlement | PostgreSQL |
| Transactional | user/business state | PostgreSQL |
| Analytical | historical market/metrics | ClickHouse و در موارد research DuckDB/Parquet |
| Event | durable business events | NATS JetStream + outbox record |
| Artifact | reports/models/datasets/raw evidence | object/artifact storage |
| Cache | acceleration/ephemeral | Redis |

PostgreSQL برای consistency و transactional semantics است؛ ClickHouse برای analytical time-series و aggregation حجیم؛ Redis برای acceleration؛ DuckDB برای local/research workloads که portability و columnar analysis مهم است.

### اصل ownership

برای هر data entity باید دقیقاً مشخص شود:

`owner → schema → writer → readers → retention → revision policy → deletion policy → audit policy`

---

## 7. Market Data و حقیقت تاریخی

هر observation باید حداقل هویت provider، instrument، venue/source، event time، ingestion time و availability/publication semantics داشته باشد.

### چهار زمان مهم

- `event_time`: زمان وقوع داده در بازار.
- `publication_time`: زمان انتشار توسط منبع، اگر موجود باشد.
- `available_at`: زمانی که داده برای CFIP واقعاً قابل استفاده بوده است.
- `ingested_at`: زمان ورود به سیستم.

این چهار زمان را نباید بدون دلیل یکی کرد.

### Revision

اگر provider مقدار گذشته را اصلاح کرد، مقدار قبلی نباید بی‌ردپا overwrite شود. revision identity، effective time و provenance باید نگه داشته شود.

### Dataset identity

هر backtest یا training run باید dataset version، provider revisions، universe definition، feature versions و execution assumptions را ثبت کند.

---

## 8. PIT و Replay

PIT یعنی بازسازی دقیق آنچه در زمان تصمیم قابل مشاهده بوده است، نه صرفاً query کردن داده‌ای که امروز برای گذشته موجود است.

برای هر decision time `t`:

`Visible(t) = {records | available_at <= t}`

اگر universe، خبر، fundamental، indicator یا provider correction بعداً ایجاد شده باشد، نباید در تصمیم تاریخی زودتر دیده شود.

Replay باید event ordering deterministic داشته باشد. tie-breaker، sequence، clock، late arrival و correction باید مشخص باشند.

### الزامات Replay

- snapshot identity
- deterministic clock
- deterministic ordering
- provider/revision identity
- feature/engine versions
- execution assumptions
- fees/spread/slippage
- random seed در صورت وجود randomness
- output manifest

---

## 9. Engine architecture

هر engine دارای:

`engine_id + version + descriptor + inputs + parameters + output schema + registry + implementation + fixtures + tests`

برای `(engine_id, version)` فقط یک semantic implementation مجاز است. live، replay و backtest باید از همان canonical implementation استفاده کنند یا adapter رسمی داشته باشند.

### FVG lifecycle

FVG باید lifecycle رسمی داشته باشد:

`candidate → formed → qualified → active → mitigated/filled → invalidated → archived`

تعریف formation، boundary، ordering، timeframe context و invalidation باید یک‌بار در canonical engine ثبت شود. UI نباید FVG را دوباره محاسبه کند.

### Order Block

باید تعریف دقیق origin، displacement، validation، mitigation و invalidation داشته باشد و با structure engine قرارداد روشن داشته باشد.

### MTF

هر signal باید timeframe خود را همراه با higher/lower timeframe evidence مشخص کند. تبدیل 15m، 1h، 4h و غیره باید بر اساس duration واقعی bar باشد؛ نام timeframe نباید صرفاً label UI باشد.

---

## 10. Indicators، Signals و Consensus

Indicator خروجی deterministic یا versioned feature است؛ signal یک hypothesis/action candidate است؛ consensus یک لایه aggregation است.

زنجیره:

`structure → features/indicators → independent analyses → signal candidates → evidence checks → consensus → final structured answer`

Consensus باید source vote، weight، independence، conflict، freshness و confidence را ثبت کند. نباید با جمع کردن duplicate outputs مصنوعاً confidence را بالا برد.

### پاسخ نهایی تحلیل

یک پاسخ نهایی باید ساختاریافته باشد:

- direction
- entry zone / trigger
- stop-loss
- target(s)
- invalidation
- risk budget
- position size
- leverage constraint
- confidence/evidence
- timeframe
- timestamp
- data freshness

این خروجی «execution authority» نیست.

---

## 11. Risk و Position Sizing

حداقل ورودی‌ها:

`equity + risk_budget + entry + stop + contract_spec + leverage + fees + slippage + broker_constraints`

فاصله stop و ارزش هر واحد باید از instrument specification بیاید؛ quantity نباید با یک فرمول ثابت و بدون توجه به symbol/broker محاسبه شود.

ریسک تحلیلی و ریسک اجرای واقعی جداست. اگر broker constraints نامشخص باشد، سیستم باید وضعیت را `UNKNOWN/UNAVAILABLE` اعلام کند، نه اینکه مقدار فرضی تولید کند.

---

## 12. Backtest

Backtest باید بین signal correctness و execution realism تفکیک کند.

حداقل execution model:

- order type
- fill timing
- spread
- slippage
- fees
- latency
- liquidity constraint
- partial fill در صورت نیاز
- market session
- position/account state

Walk-forward، embargo، out-of-sample و PIT باید برای جلوگیری از leakage در research فعال باشند.

نتیجه باید شامل raw trades، orders، positions، equity curve، assumptions و manifest باشد؛ یک عدد return به‌تنهایی evidence نیست.

---

## 13. Outcome، Attribution، Calibration و Drift

هر prediction یا signal باید بتواند بعداً به outcome متصل شود.

`prediction → decision → realized path → outcome → attribution → calibration → drift`

Attribution باید مشخص کند نتیجه به کدام engine، feature، signal، regime، timeframe و data source مرتبط بوده است.

Calibration باید با cohort و horizon مشخص انجام شود. Drift باید data drift، feature drift، prediction drift و outcome/performance drift را از هم جدا کند.

هیچ مدل یا strategy صرفاً به‌دلیل یک دوره عملکرد خوب نباید خودکار به production منتقل شود.

---

## 14. Smart Search و Research Intelligence

pipeline مرجع:

`Query → Policy → Planner → Expansion → Retrieval(BM25 + Vector) → Fusion → Reranker → Evidence Assembly → Reasoning → Citation Verification → Answer`

Research Fabric:

`ingestion → normalization → extraction → classification → deduplication → provenance → indexing → retrieval → evidence graph → synthesis → verification → feedback`

منابع خارجی untrusted هستند. محتوا نباید مستقیماً دستور tool execution تولید کند. citation باید قابل بازگشت به source artifact باشد.

### Research record

هر نتیجه تحقیق باید dataset/source snapshot، زمان تحقیق، query، sources، model version، prompt policy، citations و limitations را ثبت کند.

---

## 15. Open-source reuse

هدف این نیست که CFIP همه‌چیز را از صفر بسازد. برای هر capability باید ابتدا بازار open-source بررسی شود.

طبقه‌بندی:

- **Integrate:** component با مرز مناسب تقریباً آماده است.
- **Adapt:** هسته مناسب است ولی adapter/integration لازم است.
- **Reference:** ایده/الگو مفید است ولی dependency مستقیم مناسب نیست.
- **Rewrite-Minimal:** بخش کوچک و حیاتی را مستقل پیاده می‌کنیم.
- **Reject:** ریسک، license، maturity، معماری یا fit نامناسب.

### معیارها

license compatibility، maintenance، release discipline، security، dependency risk، API stability، tests، documentation، bus factor، performance، extensibility، persistence model، operational burden و domain fit.

### نمونه‌های تحقیق‌شده در 2026-09-16

این موارد «گزینه تحقیق» هستند، نه الزام ادغام:

1. **Open Papertrade**: نمونه‌ای برای paper trading، backtesting و RAG مالی citation-aware؛ به‌دلیل AGPL و معماری محصولی آن باید قبل از هر reuse مستقیم بررسی license و boundary انجام شود. citeturn0search0
2. **FINSABER-2**: نمونه reusable برای backtesting با execution timing، slippage، liquidity cap و artifact manifest؛ برای الهام از قرارداد backtest و result artifact مناسب است و نباید بدون بررسی license/dependency وارد هسته CFIP شود. citeturn0search1
3. **FinResearch-Agent**: نمونه FastAPI/SQLAlchemy/Timescale و research reproducibility؛ برای مقایسه workflow و contract مفید است. citeturn0search3
4. **TradingAgents**: نمونه multi-agent finance با checkpoint، decision log و multi-provider model support؛ برای agent orchestration و governance research می‌شود استفاده کرد، نه به‌عنوان domain authority. citeturn0search4
5. **Backtrader derivative ecosystem**: برای مقایسه event-driven/vectorized backtest، indicators و data-source adapters مفید است؛ suitability و license باید جداگانه بررسی شود. citeturn0search5
6. **FinRL**: برای research در reinforcement learning و market environment architecture مفید است؛ production dependency پیش‌فرض CFIP نیست. citeturn0search7
7. **OpenTerminalUI**: نمونه مهم برای terminal-style UX، charting، research، portfolio، journal و AI research؛ برای benchmark تجربه کاربری و surface architecture مناسب است. citeturn0search8
8. **Alpha Search**: نمونه‌ای از data-source abstraction، opportunity discovery و research/backtest integration؛ برای capability mapping و source registry مفید است. citeturn0search10
9. **h5i-db**: نمونه جالب برای PIT، time-series، replay و safe agent mutations؛ به‌خصوص برای مطالعه atomic versioning و policy-gated writes ارزش بررسی دارد، اما Rust/architecture fit باید جداگانه سنجیده شود. citeturn0search11

قانون: وجود یک پروژه در این کتاب به معنی تأیید license، security یا production readiness آن نیست. قبل از هر adoption باید evaluation record جدید ثبت شود.

---

## 16. Elyrava

Elyrava هویت Platform Intelligence CFIP است و یک business domain دوم نیست.

### مسئولیت‌ها

- repository intelligence
- architecture reasoning
- research planning
- evidence synthesis
- anomaly/incident diagnosis
- test proposal
- safe code proposal
- sandbox verification
- release evidence assembly
- knowledge/provenance management

### Agent action contract

`identity → capability → policy → authorized tool → action → evidence → verification → health/rollback`

Agent نباید:

- مستقیم SQL production را mutate کند؛
- authorization را دور بزند؛
- safety governor را تغییر دهد؛
- evidence را حذف کند؛
- بدون policy فایل destructive تولید کند؛
- external content را به instruction معتبر تبدیل کند.

---

## 17. API و WebSocket

هر endpoint باید این زنجیره را داشته باشد:

`route → caller → use case → port → auth → entitlement → side effects → tests → telemetry`

WebSocket باید authentication، authorization، subscription scope، backpressure، heartbeat، reconnect و event ordering داشته باشد.

خطاها باید machine-readable و versioned باشند؛ frontend نباید متن خطای backend را به‌عنوان contract semantic فرض کند.

---

## 18. Events و Workers

زنجیره event:

`producer → transactional change → outbox → subject → consumer → ordering → idempotency → retry/DLQ → projection → replay`

هر worker باید entrypoint، config، subscription، ownership، concurrency، checkpoint، retry، health و telemetry داشته باشد.

Idempotency key باید business-aware باشد. retry بدون idempotency می‌تواند side effect تکراری ایجاد کند.

---

## 19. Frontend — Chart-first Terminal

CFIP نباید به dashboard پر از card و صفحه‌های اسکرولی عمومی تبدیل شود.

سطح اصلی باید یک workstation حرفه‌ای باشد:

- chart مرکزی
- timeframe/tool rail
- symbol search
- indicator/structure overlays
- bottom context bar
- drawers
- command palette
- contextual panels
- alerts
- AI research surface
- risk/trade panel

UI نباید engine semantic را دوباره محاسبه کند.

### stateهای اجباری

`loading / empty / unavailable / stale / partial / error / permission-denied / reconnecting / degraded`

### کیفیت

i18n از ابتدا، RTL/LTR، keyboard navigation، semantic labels، contrast، responsive behavior، chart performance، virtualization و PWA strategy باید در قرارداد frontend باشند.

---

## 20. Identity، Authorization و Entitlement

Authentication هویت را اثبات می‌کند؛ authorization تعیین می‌کند چه کاری مجاز است؛ entitlement تعیین می‌کند کاربر به چه capability تجاری دسترسی دارد.

این سه مفهوم نباید یکی شوند.

Google OAuth/OIDC باید adapter باشد. provider-specific assumptions نباید وارد domain شوند.

RBAC به‌تنهایی برای policyهای پیچیده کافی نیست؛ resource، action، tenant/user، entitlement، environment و risk context می‌توانند در decision دخیل باشند.

---

## 21. Crypto Billing

flow مرجع:

`checkout → payment intent → address/invoice → observed transfer → confirmation/finality → settlement → subscription → entitlement activation → expiry/renewal → reconciliation`

هر مرحله باید idempotent، auditable و قابل reconciliation باشد.

مشاهده transaction به‌تنهایی settlement نیست. confirmation policy، chain/network، asset، amount، recipient، memo/tag در صورت وجود و finality باید بررسی شوند.

Subscription و entitlement نباید مستقیماً از frontend payment callback فعال شوند.

---

## 22. Admin، Provider و Broker

هیچ provider/broker نباید به‌صورت پراکنده در کد hardcode شود.

Admin باید بتواند، طبق policy:

- provider enable/disable
- credentials reference
- priority/fallback
- rate limits
- data freshness thresholds
- broker leverage/specification
- feature flags
- entitlement plans
- notification policies
- retention
- operational controls

را مدیریت کند.

Secrets باید در secret boundary باشند و در UI یا logs نمایش داده نشوند.

---

## 23. ML/GenAI Governance

برای هر model:

`model_id + version + provider + artifact + dataset + evaluation + policy + deployment state`

برای هر dataset:

`dataset_id + revision + provenance + license + time coverage + PIT policy + quality report`

GenAI telemetry باید trace، model/provider، token/cost metrics در صورت امکان، latency، tool calls و evaluation linkage داشته باشد؛ ولی secret و user-sensitive content نباید بی‌دلیل در telemetry ذخیره شود.

Safe auto-promotion فقط برای تغییرات کم‌خطر و با health guard، canary، evaluation threshold و rollback مجاز است. تغییرات حساس باید approval queue داشته باشند.

---

## 24. Security

Threat model باید حداقل شامل:

- credential theft
- session abuse
- broken authorization
- webhook/payment forgery
- provider compromise
- supply-chain attack
- prompt injection
- tool abuse
- data poisoning
- replay attack
- event duplication
- SSRF
- path traversal
- secret leakage
- destructive agent action

باشد.

Security controls باید در boundary اعمال شوند، نه فقط در UI.

Audit event باید actor، action، target، policy decision، timestamp، correlation id و outcome را ثبت کند.

---

## 25. Privacy و Data Residency

داده‌ها باید از نظر classification جدا شوند:

`public / internal / confidential / personal / secret / regulated`

برای هر کلاس retention، encryption، access، export، deletion و residency مشخص می‌شود.

Global architecture نباید فرض کند همه داده‌ها آزادانه بین regionها حرکت می‌کنند. user data، payment data، raw market data و telemetry می‌توانند policyهای متفاوت داشته باشند.

---

## 26. Observability و Reliability

OpenTelemetry ستون observability است.

سه سیگنال اصلی:

- traces
- metrics
- logs

هر request/event/job باید correlation context داشته باشد.

SLOها باید برای capability تعریف شوند؛ مثلاً API latency، realtime freshness، event lag، worker recovery و data freshness.

### Reliability

backup فقط وقتی معتبر است که restore تست شده باشد.

باید مشخص باشد:

`RPO + RTO + backup frequency + retention + restore procedure + failover + rollback`

---

## 27. Performance و Global Scale

Scale به معنی «microservice زیاد» نیست.

اصول:

- stateless regional API تا حد امکان
- partitionable workers
- explicit ownership/checkpoint
- bounded queues
- backpressure
- workload isolation
- cache با TTL و invalidation policy
- database partitioning/ordering مناسب
- analytical workload separation
- regional residency
- measured capacity

قبل از ادعای global readiness باید load profile، p50/p95/p99، throughput، concurrency، event lag، storage growth و cost/unit اندازه‌گیری شوند.

---

## 28. Testing

هر capability باید از چند سطح عبور کند:

1. unit
2. contract
3. integration
4. E2E
5. negative/security
6. recovery
7. PIT/replay
8. performance

برای engines، golden fixtures ضروری‌اند. برای data، fixture باید revision و availability semantics داشته باشد. برای event، duplicate/out-of-order/retry تست شود.

---

## 29. CI/CD و Supply Chain

CI باید حداقل شامل:

- formatting/lint
- type checking
- unit/contract/integration tests
- import/compile integrity
- dependency audit
- secret scanning
- container build
- migration validation
- frontend build
- accessibility smoke checks
- artifact integrity

Dependency upgrade باید release notes، compatibility و security impact داشته باشد. prerelease/nightly/canary بدون justification وارد baseline نمی‌شود.

---

## 30. Repository Governance

هر تغییر باید trace داشته باشد:

`issue/request → plan → files → tests → evidence → commit → release`

اسناد canonical باید در repository باشند و حافظه پروژه در هر release به‌روز شود.

فایل خالی، marker-only، duplicate یا operationally-empty باید در audit شناسایی شود.

---

## 31. D1 تا D11

**D1 API/WS:** route تا telemetry کامل.

**D2 Events:** producer تا replay کامل.

**D3 Data/PIT:** schema تا integrity کامل.

**D4 Engines:** identity تا composition کامل.

**D5 Workers:** entrypoint تا recovery کامل.

**D6 Frontend:** route تا tests/telemetry کامل.

**D7 Tests:** unit تا performance/recovery کامل.

**D8 Policy/config:** hardcode تا deployment/test کامل.

**D9 Adapters:** provider تا lifecycle tests کامل.

**D10 Operations:** SLO تا DR/rollback/residency کامل.

**D11 Reconciliation:** source evidence، registry، parity، manifest، ADR و repository باید با هم سازگار باشند.

---

## 32. Release Governance

Gate 0 اجازه engineering کنترل‌شده و reversible را می‌دهد، اما live/production behavior تا بسته شدن evidenceهای مربوطه آزاد تلقی نمی‌شود.

هر release باید:

- کل repository را audit کند؛
- regressionهای قدیمی را دوباره بررسی کند؛
- FVG و engine parity را verify کند؛
- worker/import/runtime boot را verify کند؛
- missing/zero-byte/marker-only files را بررسی کند؛
- dependency/security را بررسی کند؛
- frontend UX/a11y/i18n را بررسی کند؛
- telemetry و notifications را بررسی کند؛
- admin proposal queue و autonomy policy را بررسی کند؛
- project memory و release document را به‌روز کند.

---

## 33. ماتریس capability

برای هر capability این ستون‌ها اجباری‌اند:

| Capability | Context | Contract | Implementation | Evidence | Tests | Dependency | Gate | State |
|---|---|---|---|---|---|---|---|---|
| Market ingestion | Market Data | data contract | provider adapter | runtime trace | integration | provider | D3/D9 | TBD |
| PIT | Historical Truth | PIT query | snapshot/revision engine | replay fixture | PIT | ClickHouse/DuckDB | D3 | TBD |
| FVG | Structure | engine schema | canonical engine | golden fixture | unit/replay | market data | D4 | TBD |
| Consensus | Signals | consensus schema | aggregator | decision artifact | integration | engines | D4 | TBD |
| Position sizing | Risk | sizing contract | risk service | deterministic case | unit | instrument/broker | D4/D9 | TBD |
| Search | Research | search contract | hybrid retrieval | citation artifact | E2E | index | D1/D6 | TBD |
| Elyrava | Platform Intelligence | agent action contract | governed orchestrator | audit trail | security/recovery | tools | D8/D10 | TBD |
| Billing | Entitlement | payment contract | settlement workflow | reconciliation | integration | chain/provider | D8/D9 | TBD |

`TBD` عمداً به‌عنوان وضعیت واقعی باقی می‌ماند تا بدون evidence به `VERIFIED` تبدیل نشود.

---

## 34. نمودارهای اصلی

### Request

`Browser → Next.js → API → AuthZ/Entitlement → Application → Domain → Port → Adapter → Storage/Event`

### Market data

`Provider → Adapter → Raw observation → Normalization → Quality → Revision/PIT → Analytical store → Engine → Signal → UI`

### Durable event

`Transaction → Outbox → NATS JetStream → Consumer → Idempotency → Projection → Notification/Analytics`

### Research

`Query → Planner → Retrieval → Evidence → Reasoning → Citation verification → Research artifact`

### Elyrava

`Intent → Policy → Plan → Authorized tool → Sandbox → Evidence → Verification → Proposal/Action → Health → Rollback`

---

## 35. Roadmap منطقی

### Phase A — Contract Foundation

identity، config، domain contracts، instrument identity، data contracts، event contracts، repository governance.

### Phase B — Truth Layer

market ingestion، provenance، revision، PIT، dataset manifests، replay.

### Phase C — Analytical Kernel

structure، FVG، OB، MTF، indicators، signals، consensus، risk.

### Phase D — Research

search، research fabric، backtest، attribution، calibration، drift.

### Phase E — Product

chart terminal، notifications، journal، admin، entitlement، billing.

### Phase F — Elyrava

research intelligence، engineering intelligence، governed agents، sandbox و safe automation.

### Phase G — Scale

regionalization، capacity، resilience، residency، cost، DR و operational maturity.

هیچ phase صرفاً به دلیل تمام شدن فایل‌ها complete تلقی نمی‌شود؛ closure با capability evidence انجام می‌شود.

---

## 36. Definition of Done

یک قابلیت زمانی Done است که:

- contract دارد؛
- owner مشخص دارد؛
- domain invariant مشخص دارد؛
- implementation دارد؛
- persistence/event semantics مشخص دارد؛
- authorization و entitlement در صورت نیاز اعمال شده؛
- tests کافی دارد؛
- telemetry دارد؛
- failure/recovery state دارد؛
- documentation دارد؛
- evidence قابل audit دارد؛
- regression بررسی شده؛
- در capability matrix ثبت شده؛
- release gate آن بسته شده است.

---

## 37. نتیجه معماری

CFIP باید یک سیستم «feature collection» نباشد. هسته آن باید یک سیستم evidence-driven باشد که بتواند بگوید:

**چه داده‌ای داشتیم، در چه زمانی داشتیم، چه چیزی از آن استخراج کردیم، کدام engine آن را تحلیل کرد، چه شواهدی وارد تصمیم شد، چه ریسکی محاسبه شد، چه نتیجه‌ای رخ داد، و بعداً چه چیزی از آن یاد گرفتیم.**

Elyrava این زنجیره را هوشمندتر می‌کند، اما authority را از domainها نمی‌گیرد. Open-source به‌عنوان شتاب‌دهنده استفاده می‌شود، اما ownership قراردادها و invariants در CFIP باقی می‌ماند. Global scale با evidence اثبات می‌شود، نه با نام فناوری‌ها.

این مدل، مبنای معماری، implementation، audit، release و تکامل بعدی CFIP است.
