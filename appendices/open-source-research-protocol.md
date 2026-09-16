# Open-Source Research Protocol

This book intentionally records the reuse methodology rather than freezing a potentially stale list of repositories. The live candidate registry must be refreshed from GitHub/upstream sources before adoption.

## Candidate record

`name, repository, license, last release, maintenance activity, security history, dependencies, language/runtime, architecture, persistence model, extensibility, API stability, tests, documentation, operational complexity, performance evidence, scalability evidence, CFIP capability, decision, rationale, pinned version, review date`.

## Review procedure

1. Define the CFIP capability and contract before searching.
2. Search GitHub broadly and by exact capability terms.
3. Prefer maintained projects with clear licenses and releases.
4. Inspect source, tests, documentation and operational model.
5. Check known security advisories and dependency exposure.
6. Benchmark only where workload characteristics justify it.
7. Compare integration cost with minimal in-house implementation.
8. Select Integrate/Adapt/Reference/Rewrite-Minimal/Reject.
9. Put the decision behind a CFIP-owned port.
10. Record version and review date.

## Reuse anti-patterns

Do not select the repository with the largest star count automatically. Do not import a whole framework to obtain one helper. Do not copy internal data models into the domain. Do not accept abandoned dependencies because they appear feature-rich. Do not call a project “production ready” without evidence for the actual CFIP workload.

## Research domains

Search, document parsing, feeds, extraction, embeddings, reranking, market data, technical analysis, backtesting, workflow, eventing, observability, identity, policy, billing, localization, charting, testing, load testing, model evaluation and experiment tracking should all be evaluated through the same protocol.
