# CFIP Book

این repository مرجع مستندات معماری و اجرای CFIP است و باید به‌عنوان **canonical living documentation** نگهداری شود.

## مراجع اصلی

- `CFIP-COMPLETE-BOOK.md` — کتاب کامل معماری، مهندسی، اکوسیستم، contracts، data truth، trading، research، Elyrava، security، billing، testing، operations، migration و roadmap.
- `CFIP-OSS-INTEGRATION-MASTER-MATRIX.md` — رجیستری اجرایی OSS: capability → contract → candidate → decision → gate → evidence → adoption.
- `CFIP-KEY-CONTINUATION-PROMPT.md` — prompt مرجع برای ادامه منظم کار در چت‌های بعدی، با anti-loop rules و progress protocol.
- `CFIP-PROGRESS-2026-09-16.md` — گزارش دقیق آخرین iteration و وضعیت evidence.
- `BOOK-MANIFEST.json` — مشخصات machine-readable کتاب.

## Scope

کتاب ۳۰ حوزه مرجع CFIP را پوشش می‌دهد. ماتریس OSS نیز candidateهای فعلی را در سطح capability دسته‌بندی می‌کند:

> **CFIP owns contracts/domain semantics/core IP/governance; OSS provides reusable implementation behind explicit adapters.**

`cforex-platform` عمداً و دائماً خارج از معماری مقصد است. منبع مهاجرت/رفتار `CForex` و مقصد پیاده‌سازی `CFIP` است.

## روش ادامه کار

هر iteration باید:

`Current Repo → Docs → CForex Evidence → Contract → OSS Gate → Implementation → Tests → Evidence → Progress → Next Slice`

را دنبال کند. تعداد فایل/LOC معیار progress نیست. هیچ OSS فقط به دلیل محبوبیت یا وجود در GitHub وارد baseline نمی‌شود.

## کیفیت و جلوگیری از چرخه تکراری

این repository یک canonical source برای architecture و OSS decisions نگه می‌دارد. اسناد جدید فقط وقتی اضافه می‌شوند که capability/evidence/decision/release state جدیدی ایجاد کنند یا یک contract را دقیق‌تر کنند. قبل از هر ادامه، وضعیت واقعی GitHub باید دوباره خوانده شود.

## Release

2026-09-16 — canonical book baseline + OSS integration master matrix + continuation protocol.
