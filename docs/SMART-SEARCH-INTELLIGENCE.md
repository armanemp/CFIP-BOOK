# CFIP Smart Search Intelligence — Reference Architecture

## 1. Scope

Smart Search is the research/retrieval substrate of CFIP. It is not a single search box: it is a measurable pipeline from intent to evidence-backed answer.

`Query → Policy → Planner → Query expansion → Lexical + Vector retrieval → Fusion → Reranking → Evidence selection → Synthesis → Citation verification → Response`

## 2. Retrieval architecture

### Lexical

BM25 remains essential for exact names, identifiers, abbreviations, rare terms and domain vocabulary.

### Semantic

Dense retrieval handles paraphrase and semantic similarity. Embeddings are versioned and tied to dataset/index metadata.

### Hybrid fusion

OpenSearch supports hybrid search combining keyword and semantic clauses. Score normalization and rank-based reciprocal rank fusion (RRF) are both viable mechanisms; the choice is workload-dependent and must be evaluated with a judgment set. citeturn0search0turn0search1turn0search3

RRF is attractive when clause score scales are not directly comparable because it uses ranks rather than raw scores. Fusion depth, shard topology and query distribution must be included in experiments. citeturn0search1

### Reranking

Reranking is a separate stage so candidate recall can be optimized independently from final precision. OpenSearch supports cross-encoder and other reranking approaches. citeturn0search2

## 3. Evidence and provenance

Every evidence item should carry:

- stable source identifier
- canonical URL or source locator
- retrieval timestamp
- publication timestamp when available
- content hash
- parser/extractor version
- dataset/index version
- source quality and freshness signals
- transformation lineage

Important claims should be traceable to evidence. If evidence is insufficient, the system should abstain or explicitly communicate uncertainty rather than fabricate support.

## 4. Freshness

Freshness is domain-specific. News, market conditions, prices, product documentation and security information have different freshness budgets. A freshness gate should prevent stale evidence from silently supporting current claims.

## 5. Query planning

Planner responsibilities:

1. classify intent and risk
2. detect temporal constraints
3. select source domains
4. generate retrieval branches
5. assign latency/cost budget
6. determine evidence requirements
7. decide whether browsing/tool calls are necessary
8. enforce tenant and policy filters

## 6. Evaluation

Minimum offline evaluation set:

- representative query corpus
- explicit relevance judgments
- freshness-sensitive queries
- adversarial/ambiguous queries
- citation-required queries
- multilingual/RTL cases where relevant

Metrics:

| Layer | Metrics |
|---|---|
| Candidate retrieval | Recall@k, MRR |
| Ranking | nDCG@k, Precision@k |
| Reranking | nDCG lift, latency delta |
| Evidence | citation coverage, source quality, contradiction rate |
| Answer | faithfulness, completeness, abstention quality |
| Freshness | age-weighted relevance |
| Runtime | p50/p95/p99, timeout/error rate |

## 7. Search quality workbench

Every ranking change should be evaluated as an experiment with frozen query/judgment data, configuration version, index version and reproducible results. Never treat a single aggregate score as sufficient evidence.

## 8. Data plane

Connectors → raw object store → parser → canonical document → deduplication → chunking → metadata → embedding → lexical/vector indexes.

Raw artifacts remain recoverable so derived indexes can be rebuilt.

## 9. Control plane

Provider/model/index configuration, budgets, feature flags, policies, source allowlists, tenant isolation, audit and approval queues are configuration/domain state, not hardcoded UI constants.

## 10. Security

- SSRF-safe fetching and redirect controls
- content-type/size/time limits
- sandboxed parsing for risky formats
- prompt-injection resistance
- untrusted-content isolation
- secret isolation
- tenant-aware authorization
- audit for privileged actions

## 11. Observability

OpenTelemetry is the common instrumentation layer for traces, metrics and logs. citeturn0search4

Trace attributes should connect query, source, retrieval branch, index, reranker, model, tool, dataset and deployment versions without leaking secrets or sensitive content.

## 12. Release gates

No release is complete until the whole repository is checked for runtime integrity, imports, tests, empty/marker-only files, security, performance, frontend quality, data migrations, contracts, observability, documentation and rollback.

## 13. Technology boundary

The architecture favors replaceable providers. OpenSearch, a vector engine, a reranker, an LLM provider, a market-data provider or an object store must not become an accidental domain dependency. Ports/adapters and versioned contracts are mandatory where replacement is plausible.

## 14. Current reference

This document is the conceptual reference for the ecosystem pages in the repository. Detailed registries live under `data/`; navigable architecture surfaces live at repository root.
