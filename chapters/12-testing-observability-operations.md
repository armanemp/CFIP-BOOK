# ۱۶. تست، observability و عملیات

تست‌ها چهار دیوار دارند: unit، contract، integration و E2E؛ و چند لایه اجباری تکمیلی: negative/security، recovery، PIT/replay و performance. هیچ feature مهمی با unit test تنها production-ready نیست.

## release audit
هر release کل repository را بررسی می‌کند: import integrity، zero-byte/marker-only/operationally-empty files، runtime boot، Docker/Compose، package lock، migrations، API/WS contracts، worker entrypoints، security، performance و frontend. regressionهای شناخته‌شده مانند FVG lifecycle و worker logging import نیز باید در regression suite باقی بمانند.

## observability
OpenTelemetry برای traces، metrics و logs و به‌خصوص correlation بین request، event، worker و model action استفاده می‌شود. spanها باید identityهای حساس را leak نکنند. GenAI telemetry باید latency، token/cost، model، tool calls و evaluation context را تا حد سیاست privacy ثبت کند.

## SLO
برای هر مسیر critical latency، availability، error rate، freshness و recovery objective تعریف می‌شود. alert بر اساس symptom و SLO، نه تعداد log message، طراحی می‌شود.

## operations
backup/restore به صورت عملی تست می‌شود. RPO/RTO، retention، rollback، migration strategy، capacity، on-call و incident runbook باید نوشته و exercise شوند. production readiness بدون recovery evidence ناقص است.
