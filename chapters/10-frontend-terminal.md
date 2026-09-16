# ۱۲. رابط کاربری: chart-first terminal

محیط اصلی CFIP یک terminal حرفه‌ای و chart-first است: یک نمودار اصلی با ابزارهای contextual در rail، bottom bar، drawer، modal، popup و menu. dashboardهای کارت‌محور و صفحه‌های اسکرولی نباید تجربه اصلی را تعریف کنند.

Next.js 16، React، TypeScript و Tailwind لایه experience را می‌سازند و Lightweight Charts موتور chart است. داده realtime، historical و analytical باید state machine مشخص داشته باشد.

## حالت‌های UX
loading، ready، empty، unavailable، stale، partial، error، permission-denied و reconnecting باید از هم قابل تشخیص باشند. stale data نباید با live data شبیه‌سازی شود.

## chart semantics
instrument/timeframe، cursor، visible range، overlays، FVG/OB/structure، signal، entry/SL/TP، replay state و annotations باید modelهای مشخص داشته باشند. rendering نباید منطق domain را دوباره پیاده کند.

## accessibility و i18n
Keyboard navigation، focus management، semantic labels، contrast و screen-reader behavior برای ابزارهای اصلی لازم است. i18n از ابتدا برای LTR/RTL و زبان‌های متعدد طراحی می‌شود؛ متن user-facing و تنظیمات نباید hardcode شوند.

## performance
bundle، hydration، rendering frequency، websocket fan-out و chart update rate باید اندازه‌گیری شوند. virtualisation و throttling فقط با benchmark استفاده شوند. mobile/responsive layout باید terminal را از کار نیندازد.
