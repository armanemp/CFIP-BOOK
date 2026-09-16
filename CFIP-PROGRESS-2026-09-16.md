# CFIP Progress — 2026-09-16

## وضعیت

**Stage:** Capability discovery / independent CFIP control plane  
**Status:** Active  
**Target:** `armanemp/CFIP`  
**Capability source:** `armanemp/CForex`  
**Canonical intelligence:** Elyrava

> اصل این iteration: CForex فقط source کشف capability است؛ CFIP مستقل طراحی و ساخته می‌شود.

## این iteration چه شد؟

### 1. وضعیت واقعی `CFIP-BOOK` دوباره از GitHub بررسی شد

branch `main` بررسی شد و artifactهای فعلی شامل کتاب جامع، continuation prompt، OSS matrix، progress و README هستند.

### 2. مدل استقلال CFIP تثبیت شد

تفکیک canonical اکنون صریح است:

- `CForex` → capability/requirement discovery و در موارد لازم behavioral evidence
- `OSS/GitHub` → implementation/reference candidates
- `CFIP` → architecture، contracts، semantics، governance و implementation مستقل

هیچ code، directory structure یا dependency از CForex به‌صورت خودکار target CFIP محسوب نمی‌شود.

### 3. Capability Registry اضافه شد

فایل جدید:

`CFIP-CAPABILITY-REGISTRY.md`

این فایل capabilityهای مطلوب را در 48 domain ثبت می‌کند؛ از Market Data، Instrument Identity، PIT، FVG/OB/MTF و Signals تا Risk، Backtest/Replay، Research/Search، Elyrava، ML/RL، Realtime Terminal، Billing، Security، Observability، Testing و Global Scale.

Commit:

`b04ddda373b50f43b53a70c93b0e38ae6210af27`

این registry **فهرست قابلیت است، نه فهرست implementation**.

### 4. Continuation Prompt اصلاح شد

`CFIP-KEY-CONTINUATION-PROMPT.md` اکنون صریحاً می‌گوید CForex فقط capability discovery/parity evidence است و migration/code-copy ممنوع است.

Commit:

`76749ed91075ecc3c2fe093ae94c65ea75b336d5`

### 5. CFIP repository به‌عنوان target مستقل بررسی شد

درخت واقعی `armanemp/CFIP` بررسی شد. این repository دارای ساختار مستقل CFIP و اسناد معماری/منبع خود است؛ بنابراین ادامه کار باید implementation-driven و capability-driven باشد، نه source-tree-driven.

## Evidence جدید

- `armanemp/CFIP-BOOK` branch state از GitHub خوانده شد.
- `CFIP-COMPLETE-BOOK.md` بررسی شد.
- `CFIP-KEY-CONTINUATION-PROMPT.md` بررسی و اصلاح شد.
- `CFIP-OSS-INTEGRATION-MASTER-MATRIX.md` به‌عنوان registry OSS بررسی شد.
- `armanemp/CForex` tree واقعی بررسی شد؛ commit فعلی قابل مشاهده `9008821...` است.
- `armanemp/CFIP` search/tree evidence بررسی شد.

## Capability وضعیت

در این iteration هنوز نباید از روی registry درصد implementation اعلام شود. registry تازه به‌عنوان denominator/capability inventory مستقل تثبیت شده و باید status هر capability از repository واقعی CFIP استخراج شود.

**Capability-weighted implementation progress: TBD**

## D1–D11

| Domain | وضعیت |
|---|---|
| D1 API/WS | معماری/target evidence موجود؛ closure اجرایی باید از CFIP verify شود |
| D2 Events | baseline مشخص؛ implementation evidence باید verify شود |
| D3 Data/PIT | requirement و architecture مشخص؛ runtime closure نیازمند verify است |
| D4 Engines | capabilityها ثبت شده؛ canonical implementation باید capability-by-capability verify شود |
| D5 Workers | capability mapped؛ runtime verification لازم است |
| D6 Frontend | terminal capability set مشخص؛ E2E/UI verification لازم است |
| D7 Tests | gates مشخص؛ coverage/contract evidence باید از CFIP استخراج شود |
| D8 Policy/Config | governance contract مشخص؛ implementation verification لازم است |
| D9 Adapters | port/adapter model مشخص؛ concrete adapters باید verify شوند |
| D10 Operations | operational requirements مشخص؛ runtime/DR/capacity evidence لازم است |
| D11 Reconciliation | payment/provider/replay reconciliation در scope است؛ implementation verification لازم است |

## OSS decision state

هیچ OSS در این iteration صرفاً به دلیل حضور در registry `ADOPTED` نشده است.

قاعده فعلی:

- CFIP semantics/core IP → `BUILD`
- commodity implementation → evaluate `INTEGRATE`
- external provider → `ADAPT`
- uncertain candidate → `BENCHMARK` / `REFERENCE`
- adoption → فقط پس از gates و evidence

## موارد باقی‌مانده

1. وضعیت هر capability در `armanemp/CFIP` باید استخراج و به registry متصل شود.
2. CForex باید فقط برای gap discovery و behavioral evidence مرتبط بررسی شود.
3. برای candidateهای واقعی OSS، license/version/security/compatibility/performance evidence باید ثبت شود.
4. denominator رسمی progress بعد از audit CFIP تثبیت شود.
5. foundation contracts و acceptance tests باید capability-by-capability بسته شوند.

## Anti-loop checkpoint

بازنویسی معماری یا migration plan دیگر هدف نیست. این iteration مرزهای source/capability/OSS/target را تثبیت کرد و capability registry را ایجاد کرد.

از اینجا به بعد هر iteration باید یک capability slice واقعی را در `armanemp/CFIP` به سمت closure ببرد.

## قدم بعدی دقیق

**Next slice:** audit واقعی `armanemp/CFIP` بر اساس 48 capability domain، استخراج وضعیت هر capability، شناسایی gapهای واقعی، و تولید اولین capability-weighted baseline؛ سپس انتخاب اولین foundation slice برای contract + test + implementation.
