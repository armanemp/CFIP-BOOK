# ۱۸. قراردادهای کیفیت برای frontend و backend

هر endpoint باید schema request/response و error داشته باشد و contract test آن را تثبیت کند. breaking change باید versioned یا migration-aware باشد.

Frontend باید API state را به UI state نگاشت کند و برای stale، partial و reconnect رفتار صریح داشته باشد. optimistic update فقط برای stateهایی که rollback آن‌ها روشن است.

Backend باید timeout، cancellation و transaction boundary را مشخص کند. عملیات idempotent با key صریح تعریف می‌شوند.

برای chart، data adapter باید ترتیب زمانی، duplicate، gap، correction و timezone را کنترل کند. timestamp presentation هرگز جایگزین event-time canonical نمی‌شود.
