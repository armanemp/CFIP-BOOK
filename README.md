# کتاب مهندسی CFIP

این مخزن مرجع واحد طراحی و ساخت **CForex Intelligence Platform (CFIP)** است. کتاب حاضر همه تصمیم‌های پایدار پروژه را در یک ساختار واحد جمع می‌کند تا معماری، قراردادها، داده، هوش، امنیت، تجربه کاربری، عملیات و روش استفاده از پروژه‌های متن‌باز از هم گسسته نشوند.

## وضعیت مرجع
- منبع رفتاری: `armanemp/CForex`
- مقصد: `armanemp/CFIP`
- `cforex-platform`: کنار گذاشته شده و در این معماری هیچ نقشی ندارد.
- `Elyrava`: نام فعلی Platform Intelligence؛ نام قدیمی دیگر هویت محصول نیست.
- این مخزن: کتاب و کنترل‌پلین مهندسی است، نه runtime محصول.

## هدف کتاب
این سند فقط توصیف ایده نیست؛ باید برای هر قابلیت، قرارداد، مالک، داده، مسیر اجرا، تست، شواهد، عملیات و معیار پذیرش را مشخص کند. واحد پیشرفت «قابلیت تأییدشده» است، نه تعداد فایل یا درصد ساختگی.

## اصول غیرقابل مذاکره
1. قرارداد و invariantهای دامنه متعلق به CFIP است.
2. زیرساخت بالغ تا حد امکان از پروژه‌های آماده و سالم گرفته می‌شود؛ کدنویسی اختصاصی فقط جایی انجام می‌شود که ارزش دامنه‌ای یا اتصال لازم وجود دارد.
3. Redis منبع حقیقت داده تجاری نیست.
4. Outbox پایدار پیش از fan-out پایدار رویداد قرار می‌گیرد.
5. هر engine معنایی canonical برای `(engine_id, version)` دارد؛ runtime، replay و durable projection نباید منطق تحلیلی را کپی کنند.
6. PIT و replay باید از نظر زمانی قابل اثبات باشند؛ داده‌ای که در زمان تصمیم در دسترس نبوده نباید وارد نتیجه تاریخی شود.
7. تحقیق وب و GitHub ورودی غیرقابل‌اعتماد است و باید sandbox، provenance، citation و کنترل ابزار داشته باشد.
8. عامل هوشمند حق دور زدن policy، تغییر مستقیم SQL/زیرساخت یا حذف evidence را ندارد.
9. UI اصلی chart-first و terminal-like است، نه dashboard کارتی و اسکرولی.
10. entitlement با authorization یکی نیست.
11. هر release کل مخزن را audit می‌کند، نه فقط feature تغییرکرده.

## نقشه کتاب
- `BOOK-MAP.md`: فهرست کامل فصل‌ها و روابط آن‌ها
- `chapters/`: فصل‌های مهندسی
- `appendices/`: قراردادها، چک‌لیست‌ها، ماتریس‌ها و قالب‌ها
- `data/`: داده ساختاریافته کتاب
- `index.html`: نمای مرور سریع کتاب

## وضعیت شواهد
`CONFIRMED`، `PARTIAL`، `UNVERIFIED`، `NEGATIVE-SEARCH` و `TARGET-REQUIRED` تنها وضعیت‌های معتبر شواهد هستند.

چرخه قابلیت: `MAPPED → CONTRACTED → IMPLEMENTED → VERIFIED → PARITY-VERIFIED → PRODUCTION-READY`.

## خط مبنای فنی
Python 3.14، FastAPI، Pydantic، SQLAlchemy 2، Alembic، PostgreSQL، ClickHouse، Redis، NATS JetStream، DuckDB در صورت توجیه، Next.js 16، React، TypeScript، Tailwind، TradingView Lightweight Charts و OpenTelemetry. نسخه‌های prerelease/nightly/canary بدون تصمیم صریح معماری مجاز نیستند.

## معیار تکمیل
هیچ فصل یا قابلیت زمانی کامل تلقی نمی‌شود که فقط «توصیف» شده باشد. باید owner، contract، dependency، evidence، test، failure mode، observability و rollback یا محدودیت عملیاتی آن مشخص باشد.
