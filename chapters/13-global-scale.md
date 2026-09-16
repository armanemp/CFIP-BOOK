# ۱۷. performance، مقیاس و قابلیت اطمینان

«global-scale» یک ادعا نیست؛ باید با load profile، p95/p99 latency، throughput، concurrent connections، ingestion rate، storage growth، recovery time و cost per workload سنجیده شود.

API تا حد امکان stateless و قابل scale افقی است. workerها partition و ownership صریح دارند. hot path و analytical path از هم جدا می‌شوند. backpressure، bounded queue، batching و rate limit برای جلوگیری از cascade failure ضروری‌اند.

## consistency classes
برای هر داده مشخص شود strong، read-after-write، eventual یا cacheable است. این تصمیم باید در contract باشد تا frontend و worker رفتار متفاوت را تصادفی انتخاب نکنند.

## ظرفیت
برای PostgreSQL، ClickHouse، NATS، Redis، object storage و API ظرفیت بر اساس workload اندازه‌گیری می‌شود. indexها، query plan، N+1، connection pool، memory، CPU، startup و bundle size جزو release gate هستند.

## منطقه‌ای و residency
در مقیاس جهانی می‌توان API stateless را regional کرد و ingestion/analytics را بر اساس partition و data residency جدا کرد. داده‌ای که قانون یا policy محلی محدود می‌کند نباید بی‌دلیل به region دیگر منتقل شود. replication، failover و consistency باید برای هر کلاس داده تعریف شوند.
