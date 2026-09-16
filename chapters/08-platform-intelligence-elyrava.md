# ۱۰. Elyrava و Platform Intelligence

Elyrava لایه هوش سراسری پلتفرم است، نه یک bounded context که مالک منطق بازار شود. مسئولیت آن orchestration تحقیق، تحلیل، پیشنهاد، diagnosis، code/repo research، evidence synthesis و governance-aware assistance است.

## مرز
Elyrava نباید تعریف canonical FVG، risk formula یا billing state را خودش نگه دارد. برای این امور از domain contract و toolهای مجاز استفاده می‌کند. این تفکیک جلوی دو مرجع حقیقت را می‌گیرد.

## چرخه عامل
identity → capability → policy evaluation → authorized tool → action → evidence → verification → health/rollback. هر action دارای actor، intent، scope، tool، input hash، output/evidence، timestamp و نتیجه policy است.

## self-development
عامل می‌تواند مسئله را تشخیص دهد، repository را جست‌وجو کند، proposal بسازد، patch را در sandbox اجرا کند، تست و benchmark بگیرد و evidence تولید کند. تغییر production باید governed باشد. پیشنهادهای mature وارد proposal queue می‌شوند و پس از تأیید انسانی archive می‌شوند.

## self-healing
اول health detection، سپس diagnosis، mitigation کم‌خطر و reversible، verification و در صورت شکست rollback. agent حق حذف لاگ، خاموش‌کردن governor، تغییر secret boundary یا bypass policy ندارد.

## sandbox
کد تولیدشده در محیط محدود، بدون credentialهای production و با network/tool allowlist اجرا می‌شود. artifact، test log، diff، dependency changes و security result باید ثبت شوند.
