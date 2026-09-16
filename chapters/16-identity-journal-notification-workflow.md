# ۱۶. Identity، journal، notification و workflow کاربر

User workflow باید از market context جدا ولی به آن متصل باشد. Journal entry شامل instrument، timeframe، thesis، evidence، signal snapshot، risk snapshot، decision time و outcome reference است؛ نباید بعداً با داده اصلاح‌شده بی‌صدا تغییر کند.

Notificationها باید policy-aware باشند: channel، severity، deduplication، cooldown، quiet hours، entitlement و delivery status. ارسال چندباره یک signal به علت reconnect قابل قبول نیست.

Account context می‌تواند چند broker account داشته باشد. equity، leverage و constraints هر account نسخه و زمان اعتبار دارند. UI نباید اطلاعات یک account را به دیگری نشت دهد.

Workflowهای طولانی مانند research، replay یا payment باید state machine باشند؛ transition غیرمجاز، duplicate event و timeout مسیر مشخص داشته باشند.
