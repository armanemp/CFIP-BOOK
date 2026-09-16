# 05 — Smart Search and Research Intelligence

CFIP needs a research/search fabric capable of turning heterogeneous public and configured sources into cited, freshness-aware evidence. Search is not a single vector database query.

## Canonical pipeline

`Query → Policy → Planner → Expansion → Retrieval(BM25 + Vector) → Fusion → Reranker → Evidence Assembly → Elyrava reasoning → Citation Verification → Answer`

## Retrieval layers

**Lexical:** exact terminology, symbols, error strings, dates, identifiers and domain vocabulary.

**Semantic:** embeddings for paraphrase and conceptual similarity.

**Fusion:** combine lexical and semantic candidates with deterministic provenance and rank metadata.

**Reranking:** apply a stronger relevance model to a bounded candidate set.

**Evidence:** preserve source identity, URL/document identity, retrieval timestamp, publication timestamp, content hash/revision, extraction method and applicable permissions.

## Freshness and provenance

Research evidence must distinguish publication time from retrieval time. Stale material can remain useful historically but cannot silently masquerade as current evidence. A freshness policy must be configurable and auditable.

## Search safety

External content is untrusted data. Retrieved documents cannot become executable instructions. Prompt-injection resistance, content isolation, tool authorization, citation verification and output provenance are mandatory.

## Research Intelligence Fabric

Ingestion → normalization → extraction → classification → deduplication → provenance → indexing → retrieval → evidence graph → synthesis → citation check → feedback/evaluation.

Heavy ingestion and indexing are asynchronous. Search requests have bounded latency, candidate counts and resource budgets. Large documents are processed out of the API hot path.

## Evaluation

Measure recall@k, precision/nDCG where appropriate, citation correctness, freshness compliance, duplicate rate, latency, failure rate and cost. Maintain evaluation datasets with versioned provenance. Do not declare search quality from a handful of examples.
