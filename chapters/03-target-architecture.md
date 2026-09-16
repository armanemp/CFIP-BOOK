# ۳. معماری هدف و bounded contextها

معماری منطقی CFIP از Experience به Inbound، Application، Domain، Ports و Adapters می‌رود. Domain نباید به framework، database یا provider وابسته باشد. Application orchestration را انجام می‌دهد و policy را اعمال می‌کند؛ Adapter جزئیات بیرونی را حمل می‌کند.

## contextها
Identity/Access، Entitlement/Billing، Market Data، Instruments، Time-Series، Structure، Indicators، Signals، Consensus، Risk، Execution-Support، Backtest/Replay، Research، Search، Journal، Notifications، Datasets/Provenance، Learning/Calibration، Model Governance، Platform Intelligence و Administration/Operations.

این تقسیم‌بندی به معنی microservice اجباری نیست. ابتدا boundary منطقی و ownership روشن می‌شود؛ deployment فقط وقتی جدا می‌شود که scale، failure isolation، security یا team ownership آن را توجیه کند.

## data planeها
- Control plane: policy، configuration، feature flags، registry و governance.
- Transactional plane: user، entitlement، journal، audit و state تجاری.
- Analytical plane: time-series، features، aggregates و outcomes.
- Event plane: durable messaging و replay metadata.
- Artifact plane: dataset، model، evidence، report و sandbox artifact.

## ownership
هر جدول، stream، cache key و artifact باید owner داشته باشد. shared mutable state بدون قرارداد ممنوع است. cross-context query از طریق contract یا projection انجام می‌شود، نه دسترسی پنهانی به جداول context دیگر.

## deployment
APIهای stateless می‌توانند scale افقی شوند. workerها باید ownership، concurrency و checkpoint روشن داشته باشند. persistence باید با workload خودش انتخاب شود؛ PostgreSQL برای transaction و metadata، ClickHouse برای analytical/time-series workload، Redis برای cache/coordination و NATS JetStream برای durable event transport مناسب‌اند.
