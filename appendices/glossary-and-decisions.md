# واژه‌نامه و ثبت تصمیم‌های پایدار

**CFIP:** CForex Intelligence Platform.  
**CForex:** منبع رفتاری که semantics آن برای انتقال بررسی می‌شود.  
**Elyrava:** Platform Intelligence فعلی.  
**PIT:** بازسازی وضعیت قابل مشاهده در یک زمان تاریخی با رعایت availability.  
**Replay:** اجرای دوباره یک سناریو با dataset/config/versionهای pin شده.  
**Provenance:** زنجیره منشأ و تبدیل داده/evidence.  
**Entitlement:** ظرفیت/حق محصول خریداری‌شده یا اعطا‌شده.  
**Outbox:** ثبت durable side effect/event در کنار transaction پیش از publish.  
**Canonical engine:** تنها implementation معنایی مرجع برای یک engine/version.  
**Evidence:** داده یا artifact قابل ارجاع که یک claim را پشتیبانی یا رد می‌کند.

## تصمیم‌های پایدار
- معماری مقصد CFIP مستقل از `cforex-platform` است.
- Python-first stack خط مبناست.
- chart-first terminal تجربه اصلی است.
- Redis authoritative نیست.
- durable outbox پیش از durable fan-out است.
- PIT و replay جزو core correctness هستند.
- Elyrava مالک domain semantics نیست.
- agent autonomy باید policy-bound، auditable و reversible باشد.
- open-source reuse پیش از rewrite بررسی می‌شود.

هر تصمیم جدیدی که یکی از این‌ها را تغییر دهد باید ADR جدید داشته باشد و اثر آن روی contracts، migration، tests و operations ثبت شود.
