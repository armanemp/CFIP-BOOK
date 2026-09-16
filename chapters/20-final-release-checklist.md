# ۲۰. چک‌لیست نهایی release

### مخزن
- [ ] هیچ فایل zero-byte یا marker-only بدون دلیل ندارد.
- [ ] import و entrypointهای Python سالم‌اند.
- [ ] package/lockfile و Docker build سالم است.
- [ ] migrationها قابل اجرا و rollback strategy روشن دارند.

### محصول
- [ ] مسیرهای اصلی chart، search، signal، risk، journal و notification تست شده‌اند.
- [ ] auth/authz/entitlement negative cases تست شده‌اند.
- [ ] i18n، RTL/LTR، accessibility و responsive بررسی شده‌اند.

### داده
- [ ] provenance و revision موجود است.
- [ ] PIT و replay fixture موفق است.
- [ ] leakage و future data بررسی شده است.

### هوش
- [ ] model/dataset versions pin شده‌اند.
- [ ] citation و freshness verification موجود است.
- [ ] tool permissions و agent audit ثبت می‌شود.
- [ ] rollback و health guard تست شده است.

### عملیات
- [ ] SLO/SLI و dashboard/alert تعریف شده.
- [ ] backup restore واقعاً اجرا شده.
- [ ] load/performance و failure injection در scope مناسب اجرا شده.
- [ ] incident و rollback runbook به‌روز است.

### مستندات
- [ ] ADRها، evidence register، capability matrix و release notes هماهنگ‌اند.
- [ ] وضعیت هر capability با evidence واقعی ثبت شده است.

اگر یکی از موارد critical نامشخص باشد، release باید `NOT READY` بماند؛ درصد پیشرفت جای evidence را نمی‌گیرد.
