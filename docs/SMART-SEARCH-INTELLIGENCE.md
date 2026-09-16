# Smart Search Intelligence

## 1. هدف

این سند معماری مرجع یک موتور جستجوی هوشمند را تعریف می‌کند که از ingestion و crawling تا parsing، indexing، retrieval، ranking، evidence selection، answer synthesis، citation، observability، security و governance را پوشش می‌دهد.

اصل کلیدی: **LLM جایگزین retrieval نیست؛ LLM لایه synthesis و reasoning روی evidence است.**

## 2. Pipeline مرجع

`Query → Normalize → Intent/Language → Query Expansion → Candidate Retrieval → Hybrid Fusion → Rerank → Evidence Filter → Answer Synthesis → Citation/Provenance → Cache/Telemetry`

## 3. لایه‌ها

### Data Plane
Crawler/connectors، parser، OCR، deduplication، canonicalization، chunking، metadata extraction و freshness scheduling.

### Retrieval Plane
Lexical/BM25 + vector retrieval + metadata filters + hybrid fusion + reranking + query routing.

### Intelligence Plane
Intent classification، query planning، evidence selection، synthesis، citation و confidence calibration.

### Control Plane
Provider configuration، feature flags، budgets، model registry، policy versions، audit و approval workflow.

### Observability
Tracing از query تا source/evidence/answer، latency budgets، retrieval recall، reranker lift، citation coverage و failure taxonomy.

### Security
SSRF protection، URL allow/deny policy، sandboxed fetching، secret isolation، prompt-injection resistance و tenant isolation.

## 4. معیارهای ارزیابی

| محور | معیارها | هدف |
|---|---|---|
| Retrieval | Recall@k, nDCG@k, MRR | ورود evidence درست به candidate set |
| Reranking | nDCG lift, precision@k | افزایش relevance با latency کنترل‌شده |
| Answer | Faithfulness, citation coverage | پاسخ مستند و قابل بررسی |
| Freshness | age-weighted relevance | کاهش اتکا به اطلاعات منقضی |
| Performance | p50/p95/p99 | بودجه latency برای هر stage |
| Reliability | error/timeout rate | fallback و graceful degradation |

## 5. اصول غیرقابل مذاکره

1. هر پاسخ factual مهم باید provenance داشته باشد.
2. providerها پشت interface قرار گیرند و vendor lock-in ایجاد نشود.
3. retrieval و generation مستقل benchmark شوند.
4. تغییر ranking/model باید regression suite داشته باشد.
5. fetch خارجی باید در برابر SSRF، redirect abuse و منابع ناامن محافظت شود.
6. latency هر stage باید قابل مشاهده باشد.
7. freshness بخشی از ranking و نه یک metadata تزئینی باشد.
8. پاسخ بدون evidence کافی باید downgrade، abstain یا درخواست clarification شود.

## 6. Roadmap

1. Foundation: contracts، schemas، source registry و canonical document model.
2. Ingestion: crawler/connectors، parser، dedupe، chunking و freshness.
3. Indexing: lexical + vector indexes و metadata filtering.
4. Retrieval: hybrid fusion، query routing و reranking.
5. Intelligence: evidence selection، synthesis، citations و confidence.
6. Evaluation: golden set، offline benchmark، regression gates و tracing.
7. Production hardening: security، rate limits، caching، multi-tenancy و cost controls.

## 7. نکته درباره امتیازها

امتیازهای موجود در ماتریس صرفاً برای مقایسه داخلی همین artefact هستند و نباید به‌عنوان benchmark مستقل یا ادعای قطعی عملکرد فناوری‌ها تفسیر شوند.
