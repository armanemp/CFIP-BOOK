# ۶. Market Data، identity و PIT

داده بازار باید از provider observation شروع شود و پس از normalization به canonical observation تبدیل شود. identity حداقل شامل provider، instrument، event timestamp، sequence/observation identity و revision semantics است.

سه زمان باید جدا باشند: `event_time` زمان وقوع بازار؛ `publication_time` زمان انتشار توسط منبع؛ `availability_time` زمانی که CFIP واقعاً می‌توانست داده را ببیند. PIT با availability تعریف می‌شود، نه با timestamp ظاهری کندل.

## lineage
هر dataset باید source، provider، ingestion run، schema version، normalization version، revision، checksum/identity و policy دسترسی را حمل کند. late arrival و correction نباید silently داده قدیمی را overwrite کنند؛ revision chain لازم است.

## replay
Replay case باید dataset revision، cut-off time، configuration، engine versions، feature versions، model versions و random seed در صورت نیاز را pin کند. نتیجه باید deterministic تا حد ممکن و در غیر این صورت variance آن ثبت شود.

## storage
PostgreSQL برای metadata و transactional lineage؛ ClickHouse برای حجم analytical/time-series؛ object/artifact storage برای فایل‌های خام، dataset و مدل؛ Redis برای cache. DuckDB می‌تواند در local analytical jobs و validation استفاده شود، مشروط به benchmark و ownership روشن.

## اصل ضد leakage
در backtest، training و evaluation هیچ future publication یا revised recordی که در cut-off موجود نبوده، قابل استفاده نیست. حتی featureهای محاسبه‌شده باید version و input window داشته باشند تا leakage پنهان نشود.
