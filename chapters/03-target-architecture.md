# 03 — Target Architecture

CFIP uses layered, bounded-domain architecture with explicit ports and adapters. Inbound adapters (HTTP/WebSocket/UI/events) invoke application use cases. Domain logic owns invariants. Infrastructure implements ports. No framework becomes a domain authority.

## Logical layers

**Experience:** Next.js/React terminal, i18n, accessibility, realtime presentation.

**Inbound:** REST, WebSocket, event consumers, scheduled workers.

**Application:** use cases, orchestration, authorization/entitlement checks, transaction boundaries.

**Domain:** market structure, FVG/OB, indicators, signals, consensus, risk, research, journal, billing state machines and governance contracts.

**Ports:** market data, broker, identity, model/LLM, research provider, storage, event bus, billing, notification.

**Adapters:** concrete providers, PostgreSQL/ClickHouse/Redis, NATS, OAuth, crypto settlement, model runtimes and external research systems.

## Data planes

Control plane: identity, configuration, entitlements, provider definitions, policies, governance, audit metadata.

Transactional plane: authoritative business state and state transitions.

Analytical plane: large historical/aggregate workloads.

Event plane: durable asynchronous propagation and replayable streams.

Artifact plane: large immutable datasets, research documents, model/evaluation artifacts and exports when object storage is justified.

## Bounded contexts

The target is organized around explicit capabilities rather than source folders. Typical domains are identity/access, entitlement/billing, market-data, instruments, time-series, structure, indicators, signals, consensus, risk, execution-support, backtest/replay, research, search, journal, notifications, datasets/provenance, learning/calibration, model governance, platform intelligence, administration and operations.

The exact registry in the runtime repository is authoritative; this book supplies the architectural contract.

## Dependency rule

`UI/API/event → application → domain → ports ← adapters/infrastructure`

Dependencies point inward. Domain packages cannot import FastAPI, React, database clients, vendor SDKs or transport-specific objects.

## Global deployment

Prefer stateless regional APIs, partitionable workers, explicit ownership/checkpoints, workload isolation, bounded caches, regional data-residency boundaries, asynchronous heavy workloads and measurable SLO/capacity controls. Multi-region consistency must be classified rather than assumed.
