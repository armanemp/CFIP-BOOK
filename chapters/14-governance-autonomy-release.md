# ۱۹. حاکمیت agent و autonomous engineering

خودکارسازی باید capability-bounded باشد. agent ابتدا identity و capability خود را اعلام می‌کند، policy engine اجازه را ارزیابی می‌کند، سپس فقط tool مجاز را فراخوانی می‌کند و evidence تولید می‌شود.

## سطوح عمل
مشاهده و گزارش کم‌خطر؛ پیشنهاد تغییر؛ اجرای sandbox؛ تغییر محدود و reversible؛ عملیات production حساس. سطح بالاتر به evidence و approval قوی‌تر نیاز دارد.

## ممنوعیت‌های ذاتی
دسترسی مستقیم agent به production database، secrets، infrastructure root، billing ledger یا governorهای امنیتی بدون gateway مجاز نیست. حذف evidence، تغییر audit، bypass authorization و self-escalation ممنوع است.

## proposal queue
هر proposal شامل هدف، scope، diff، dependency، test result، benchmark، security result، evidence، risk، rollback و approval state است. پیشنهاد mature قبل از اعمال production نیازمند approval است. پس از تصمیم، artifact archive می‌شود.

## self-healing
Detection → diagnosis → hypothesis → bounded mitigation → verification → rollback/escalation. هر mitigation باید idempotent و ترجیحاً reversible باشد. اگر evidence کافی نیست، agent باید متوقف و escalation کند، نه اینکه حدس را به تغییر production تبدیل کند.
