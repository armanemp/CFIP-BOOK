# 07 — Trading Intelligence and Risk

CFIP is a decision-support system. Its analytical output must be explicit about evidence, uncertainty and risk rather than pretending that a signal is a guaranteed outcome.

## Signal architecture

Market observations → normalized features → structural engines → indicator/features → signal candidates → independent evidence checks → consensus boundary → final structured answer → notification/UI → outcome attribution.

There is one authoritative analysis-consensus boundary. Individual engines may disagree; the consensus layer records evidence and disagreement instead of silently averaging incompatible semantics.

## Final trade answer

A user-facing answer should have explicit direction/state, instrument, timeframe, entry context, invalidation/stop logic, target logic where applicable, confidence/evidence fields, timestamp and provenance. Missing evidence produces an explicit unavailable/insufficient-evidence state.

## Risk and position sizing

Risk calculations are account-aware. Inputs include account equity, broker account configuration, leverage constraints, instrument contract characteristics, entry, stop distance, risk budget and applicable fees/slippage assumptions. Position sizing must be deterministic, unit-aware and validated against broker constraints.

Risk engines must distinguish analytical advice from execution authority. A calculation can be displayed without granting the system permission to place a live order.

## Backtest and attribution

Backtests require PIT-correct datasets, explicit fees/slippage assumptions, deterministic seed/configuration where stochastic components exist, and reproducible run identity. Outcomes feed calibration and drift analysis but cannot silently rewrite historical evidence.

## Journal and notifications

Journal entries preserve user intent and market context. Notifications are derived from governed signal/event contracts and must be deduplicated, rate-limited and observable.
