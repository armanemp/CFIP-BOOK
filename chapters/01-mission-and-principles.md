# ۱. مأموریت، دامنه و invariantها

CFIP یک سکوی Python-first برای تبدیل داده خام بازار، ساختار قیمت، شاخص‌ها، شواهد بیرونی و مدل‌های هوشمند به **market intelligence قابل ردیابی و قابل آزمون** است. محصول نباید صرفاً مجموعه‌ای از indicatorها یا یک chatbot باشد؛ هر پاسخ باید مسیر داده، زمان دسترسی، منطق، policy و evidence قابل بازسازی داشته باشد.

## دامنه
بازار و instrument، ingestion، normalization، structure، FVG، Order Block، MTF، indicators، signal، consensus، risk/position sizing، backtest/replay، journal، notification، research/search، dataset/provenance، calibration/drift، model governance، Elyrava، identity، entitlement، billing، admin، observability و operations.

## خارج از دامنه پیش‌فرض
CFIP در هسته خود broker execution authority نیست. اتصال به broker می‌تواند adapter باشد، اما تصمیم تحلیلی، پیشنهاد و اجرای سفارش باید از هم تفکیک شوند. همچنین هیچ UI قدیمی Laravel/PHP مبنای معماری نیست.

## invariantهای اصلی
- یک هویت canonical برای instrument در کل سیستم.
- یک تعریف canonical برای هر engine و version.
- زمان‌های event/publication/availability از هم جدا.
- state تجاری در storage مناسب خودش؛ cache هرگز source of truth نیست.
- side effectهای مهم idempotent.
- همه عملیات حساس audit trail دارند.
- خروجی هوش مصنوعی بدون provenance معتبر نیست.
- historical result باید با PIT قابل بازسازی باشد.

## اصل طراحی
هر feature ابتدا به capability map می‌رود، سپس contract، implementation، verification و در نهایت production readiness. تغییر معماری بدون ثبت تصمیم و اثر آن روی قراردادهای قبلی پذیرفته نیست.
