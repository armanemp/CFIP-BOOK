# Smart Search Intelligence

## Pipeline

`Intent → Policy → Planner → Query expansion → lexical/semantic retrieval → fusion → reranking → evidence selection → synthesis → citation verification → response`

## Retrieval

BM25 is required for exact names, identifiers, rare terminology and domain vocabulary. Dense retrieval handles semantic similarity and paraphrase. Hybrid retrieval combines both. Rank fusion is preferred to raw score arithmetic unless calibrated normalization proves superior. Reranking is an independent stage and must be justified by measured relevance lift versus latency/cost.

## Evidence object

Each evidence record should contain: stable source ID, canonical locator, retrieval time, publication time when available, content hash, parser version, dataset/index version, source quality, freshness signals and transformation lineage.

## Freshness

Freshness is a policy, not a UI decoration. News, prices, market state, security advisories, product documentation and historical research require different freshness budgets. A current-claim gate must reject or qualify evidence outside its budget.

## Planner

The planner classifies intent and risk, detects temporal constraints, selects source classes, creates retrieval branches, assigns latency/cost budgets, defines evidence requirements, applies tenant/policy filters and decides when tools are necessary.

## Evaluation

Use a frozen judgment set and versioned configuration/index. Track Recall@k, MRR, nDCG@k, Precision@k, reranker lift, latency, citation coverage, contradiction rate, faithfulness, completeness, abstention quality and freshness-adjusted relevance. Never promote a ranking change from a single aggregate score.

## Research fabric

Connectors ingest raw artifacts into durable storage; parsers produce canonical documents; deduplication and chunking create retrieval units; metadata and embeddings are versioned; indexes are rebuildable. Raw evidence remains recoverable.

## Security

Fetching requires SSRF defenses, redirect controls, content-type/size/time limits and isolated parsing. Retrieved content is untrusted data and must not become instructions. Secrets are isolated. Tenant authorization applies before retrieval and synthesis.

## Provider boundary

Search engine, embedding model, reranker, LLM, crawler and object store are replaceable adapters. Domain code must not import their SDKs directly.
