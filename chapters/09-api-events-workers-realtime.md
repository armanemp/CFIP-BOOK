# ۵. API، WebSocket، event و worker

## API
مسیر هر request باید قابل دنبال‌کردن باشد: route → caller/context → use case → port → authn → authz → entitlement → domain operation → side effect → telemetry → test. DTOهای بیرونی با domain model قاطی نمی‌شوند. خطاها ساختاریافته، versioned و قابل مشاهده‌اند.

## WebSocket
اتصال دارای authentication، authorization، subscription scope، heartbeat، reconnect، backpressure و sequence/cursor است. disconnect نباید باعث از دست رفتن معنایی eventهای durable شود. realtime فقط projection سریع است؛ source of truth از persistence/event log می‌آید.

## Event
الگوی پایدار: producer → transactional state/outbox → subject → consumer → ordering policy → idempotency key → retry/DLQ → projection → replay. Event schema باید version، event_id، aggregate identity، occurred_at، published_at، correlation/causation و producer version داشته باشد.

## worker
هر worker باید entrypoint، config، subscription، ownership، concurrency limit، checkpoint، retry policy، health signal، telemetry و recovery procedure داشته باشد. importهای ناقص، entrypoint بدون execution و workerهای marker-only شکست محسوب می‌شوند.

## resilience
retry فقط برای خطاهای transient و با backoff/jitter. poison message به DLQ. عملیات خارجی timeout و circuit policy دارند. idempotency در consumer و side-effectهای billing/notification الزامی است.
