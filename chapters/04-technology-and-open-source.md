# ۴. فناوری و استفاده از پروژه‌های آماده

خط مبنای runtime شامل Python 3.14، FastAPI، Pydantic، SQLAlchemy 2، Alembic، PostgreSQL، ClickHouse، Redis، NATS JetStream، Next.js 16، React، TypeScript، Tailwind، Lightweight Charts و OpenTelemetry است؛ DuckDB تنها در صورت وجود use-case و benchmark روشن اضافه می‌شود.

## قانون reuse
هر نیاز ابتدا در GitHub و ecosystem متن‌باز جست‌وجو می‌شود. هدف «کمترین کدنویسی اختصاصی لازم» است، نه بیشترین تعداد dependency. پروژه آماده باید از نظر license، فعالیت، release cadence، CVE/security posture، کیفیت تست، dependency graph، API stability، persistence، extensibility، performance، bus factor و هزینه عملیات بررسی شود.

## طبقه‌بندی
`Integrate`: تقریباً مستقیم و با مرز adapter. `Adapt`: با wrapper/config محدود. `Reference`: ایده یا الگو استفاده می‌شود. `Rewrite-Minimal`: فقط جزء کوچک موردنیاز بازنویسی می‌شود. `Reject`: ریسک یا عدم تناسب بیشتر از ارزش است.

## حوزه‌های جست‌وجو
API/web framework، validation، database/ORM، migrations، message broker، cache، observability، auth/OIDC، search/BM25، vector retrieval، reranking، document parsing، workflow/orchestration، market-data connectors، charting، backtesting، feature store، ML lifecycle، experiment tracking، secrets، policy، testing، browser automation، i18n، payment infrastructure و DevOps.

هیچ پروژه‌ای فقط به علت محبوبیت پذیرفته نمی‌شود. license سازگار با مدل محصول، قابلیت self-host، maintenance و security شرط پایه‌اند. وابستگی به سرویس vendor-specific نیز باید با هزینه خروج و portability ثبت شود.
