# راهبرد پیاده‌سازی و acceptance

ترتیب کار بر اساس dependency و risk است، نه ظاهر محصول: foundation/contracts → data/PIT → canonical engines → API/events/workers → intelligence/research → risk/product → security/billing → frontend → operations → governed autonomy.

## مراحل
**P0:** repository hygiene، architecture baseline، contracts، configuration و CI.  
**P1:** market data، identity، instruments، time-series، provenance و PIT.  
**P2:** engines، FVG/OB/MTF، indicators، signals و replay.  
**P3:** API/WS، events، workers، notifications، journal و risk.  
**P4:** search، research fabric، Elyrava، datasets/model governance.  
**P5:** terminal UI، auth/OIDC، entitlement و crypto billing.  
**P6:** observability، performance، DR، global deployment و hardening.  
**P7:** governed autonomy و self-healing با sandbox و proposal queue.

هر مرحله فقط وقتی بسته می‌شود که capabilityهای وابسته evidence داشته باشند. «تقریباً آماده» وضعیت release نیست.

## acceptance
برای هر قابلیت: happy path، invalid input، permission failure، dependency failure، retry، duplicate، stale data، recovery، telemetry، audit و rollback بررسی می‌شود. برای historical analytics، PIT/no-leakage و replay الزامی‌اند.

## anti-patternهای ممنوع
کپی منطق engine در frontend؛ استفاده از Redis به عنوان truth؛ direct DB access بین contextها؛ webhook به عنوان ledger؛ agent با production credentials؛ hardcoded entitlement؛ dashboard جای terminal؛ و dependency جدید بدون fit/security/license review.
