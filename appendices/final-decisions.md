# ثبت تصمیم‌های نهایی کتاب CFIP

## تصمیم‌های هویتی
- CForex منبع شواهد رفتاری است.
- CFIP مقصد است.
- cforex-platform از معماری مقصد حذف شده است.
- Elyrava نام canonical Platform Intelligence است.

## تصمیم‌های معماری
- Python 3.14 + FastAPI + Pydantic + SQLAlchemy 2 + Alembic.
- PostgreSQL برای control/transactional state.
- ClickHouse برای analytical time-series.
- Redis فقط cache/ephemeral acceleration.
- NATS JetStream برای durable event delivery با outbox.
- DuckDB در research/local analytical workload در صورت توجیه.
- Next.js + React + TypeScript + Tailwind برای frontend.
- TradingView Lightweight Charts برای chart surface.
- OpenTelemetry برای observability.
- Docker/Compose برای reproducible environments.

## تصمیم‌های domain
- یک canonical engine برای هر `(engine_id, version)`.
- FVG lifecycle یک semantic authority دارد.
- PIT و replay جزء هسته data truth هستند.
- consensus مالک محاسبه indicator/structure نیست.
- risk از execution authority جداست.
- entitlement از authorization جداست.

## تصمیم‌های AI
- agent زیر policy governor است.
- external content untrusted است.
- tool authorization مستقل از model output است.
- destructive action باید reversible و auditable باشد.
- auto-promotion فقط برای low-risk و با health guard مجاز است.

## تصمیم‌های کیفیت
- production readiness بدون evidence پذیرفته نیست.
- release audit کل repository را پوشش می‌دهد.
- missing/zero-byte/marker-only artifact باید fail شود.
- performance و global scale باید با benchmark اثبات شوند.
