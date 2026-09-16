# 10 — Chart-First Frontend Terminal

The primary interface is a professional trading terminal centered on a large chart. Avoid the conventional dashboard pattern of stacked cards and endless scrolling.

## Layout

Chart canvas is the primary workspace. Secondary capabilities appear through contextual rail tools, bottom bars, drawers, popovers, modals and menus. Panels open without destroying chart context.

## Technical contract

Next.js 16 + React + TypeScript provide the experience layer. Tailwind provides presentation primitives. TradingView Lightweight Charts provides visualization. Domain calculations remain server/domain-owned and are not reimplemented in React components.

## Terminal capabilities

Symbol/timeframe selection; multi-timeframe context; indicators; FVG/OB overlays; signals; drawing tools; replay/backtest controls; AI/research assistant; risk calculator; journal; alerts; provider/account context; settings and administration surfaces appropriate to the user's role.

## UX states

Every feature needs loading, empty, unavailable, stale, partial, error, permission-denied and reconnecting states where applicable. Realtime gaps must be visible and recoverable.

## Accessibility and i18n

Keyboard navigation, semantic controls, focus management, reduced-motion behavior, contrast and screen-reader semantics are required. User-facing strings must be localized. RTL/LTR must be structural rather than a late CSS patch.

## Performance

Keep the chart responsive through bounded subscriptions, virtualization where appropriate, memoization based on measured bottlenecks, lazy loading of secondary features and controlled rendering. Measure rather than optimizing by intuition.

## Security

Treat browser state as untrusted. Enforce authorization server-side. Do not expose secrets or privileged provider credentials to the client.
