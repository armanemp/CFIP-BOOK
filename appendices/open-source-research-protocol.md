# پروتکل تحقیق GitHub و open-source

این سند تعیین می‌کند چه زمانی باید چیزی را آماده بخریم/ادغام کنیم و چه زمانی کدنویسی کنیم.

## مرحله ۱: تعریف capability
نیاز به زبان فنی مستقل از repository نوشته می‌شود؛ مثال: «durable workflow با retry و visibility» نه نام یک پروژه.

## مرحله ۲: کشف
GitHub، package ecosystem و مستندات رسمی بررسی می‌شوند. حداقل چند candidate باید دیده شوند تا انتخاب بر اساس یک repository تصادفی نباشد.

## مرحله ۳: غربال
license، آخرین release/commit، issue health، security advisories، dependency freshness، supported runtimes، tests، docs، contributors و operational complexity ثبت می‌شوند.

## مرحله ۴: آزمایش
یک spike کوچک با workload واقعی CFIP اجرا می‌شود. latency، memory، throughput، failure recovery و integration complexity اندازه‌گیری می‌شود.

## مرحله ۵: تصمیم
`Integrate / Adapt / Reference / Rewrite-Minimal / Reject` همراه با دلیل و risk ثبت می‌شود.

## حوزه‌های اجباری جست‌وجو
Search و retrieval؛ parsing؛ workflow؛ broker/data connectors؛ backtesting؛ ML/GenAI؛ vector/lexical index؛ auth/OIDC؛ observability؛ testing؛ i18n؛ charting؛ secrets؛ payment؛ DevOps.

## قاعده مهم
کتاب می‌تواند candidateها را معرفی کند، اما تا زمانی که نسخه، license و وضعیت فعلی از منبع معتبر بررسی نشده، candidate به عنوان «وابستگی انتخاب‌شده» تلقی نمی‌شود. انتخاب باید تاریخ و evidence داشته باشد.
