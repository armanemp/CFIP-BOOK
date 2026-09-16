# ۱۷. Privacy، data governance و residency

داده user، account، payment، research و telemetry طبقه‌بندی می‌شود. data minimization، retention، access logging، export/delete policy و purpose limitation باید به schema و policy تبدیل شوند.

PII نباید در traces یا promptها به شکل غیرضروری ثبت شود. شناسه‌های داخلی pseudonymous و correlation IDs کم‌خطرتر از raw identity هستند.

Data residency باید برای region و نوع داده مشخص باشد. replication cross-region فقط با policy سازگار انجام می‌شود. backup نیز بخشی از data boundary است و نباید از قوانین production جدا فرض شود.

Third-party research content باید از user-private data جدا نگه داشته شود. agent نباید یک سند خارجی را به‌عنوان مجوز دسترسی به داده خصوصی تلقی کند.
