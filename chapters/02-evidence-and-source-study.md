# ۲. مطالعه CForex و استخراج رفتار

CForex منبع رفتاری است، نه قالب فیزیکی مقصد. مطالعه باید از UI و نام فایل عبور کند و semantics را استخراج کند: ورودی، precondition، algorithm، state transition، خروجی، خطا، side effect، persistence و observable behavior.

## روش
برای هر capability یک پرونده source-study ساخته می‌شود: نام قابلیت، مسیرهای source، entrypointها، dependencyها، مدل داده، endpoint/event، تست‌های موجود، edge caseها و شواهد runtime. سپس به contract مستقل CFIP تبدیل می‌شود.

## سلسله‌مراتب evidence
۱) implementation و تست executable؛ ۲) schema/migration/contract؛ ۳) entrypoint و composition؛ ۴) CI/config/ops؛ ۵) documentation؛ ۶) release prose. اختلاف منابع باید به نفع evidence قوی‌تر حل شود.

## parity
Parity یعنی رفتار مورد نظر حفظ شده یا آگاهانه تغییر کرده و تفاوت ثبت شده است. parity صرفاً شباهت نام یا تعداد endpoint نیست. برای قابلیت‌های حساس مانند FVG، auth، websocket، dedupe و risk باید fixtureهای قابل بازتولید داشته باشیم.

## ممنوع
`cforex-platform` نباید وارد source map، target dependency، migration plan یا architecture diagram شود. هیچ تصمیمی نباید صرفاً چون در یک snapshot قدیمی وجود داشته، به CFIP منتقل شود.

## خروجی مطالعه
هر capability در یکی از وضعیت‌های `CONFIRMED / PARTIAL / UNVERIFIED / NEGATIVE-SEARCH / TARGET-REQUIRED` قرار می‌گیرد و مرحله lifecycle آن نیز ثبت می‌شود. این دو محور نباید با هم مخلوط شوند؛ مثلاً «پیاده‌سازی‌شده ولی verification نشده» ممکن است `IMPLEMENTED + UNVERIFIED` باشد.
