# ۱۳. هویت، امنیت، policy و تنظیمات

Authentication، authorization و entitlement سه مفهوم مستقل‌اند. Authentication هویت را ثابت می‌کند؛ authorization اجازه عملیات را می‌دهد؛ entitlement تعیین می‌کند کاربر چه محصول/ظرفیتی را خریداری یا دریافت کرده است.

Google OAuth/OIDC باید adapter باشد و token/session policy در CFIP تعریف شود. secretها هرگز در source، log یا prompt agent قرار نمی‌گیرند. حداقل دسترسی، rotation، expiry، audit و separation of duties الزامی‌اند.

## threat model
اعتبارسنجی ورودی، SSRF، injection، broken access control، token theft، replay، websocket abuse، dependency vulnerability، supply-chain attack، data exfiltration، prompt injection و tool abuse باید در threat register باشند.

## policy
قواعد user-facing و operational نباید در کد به صورت magic constant پخش شوند. Configuration ownership، environment scope، default، validation، secret/non-secret classification، rollout و test باید مشخص باشد. feature flag برای تغییر behavior بدون deploy مفید است ولی نباید جای policy ثابت یا authorization را بگیرد.

## audit
عملیات حساس شامل actor، action، resource، decision، policy version، timestamp، correlation id و نتیجه را ثبت می‌کنند. evidence نباید قابل حذف بی‌ردپا باشد.
