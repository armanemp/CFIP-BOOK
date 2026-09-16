# ۸. Signal، consensus، risk و outcome

Pipeline تحلیلی باید از ساختار و feature به signal candidate برسد؛ سپس evidence مستقل، conflict و confidence بررسی شود و در یک consensus boundary به نتیجه ساختاریافته تبدیل گردد. UI نباید چند پاسخ متناقض را به جای یک contract نهایی نمایش دهد.

## risk
Position sizing باید حداقل equity حساب، risk budget، leverage broker، contract size، tick/pip characteristics، entry، stop distance، target، fee، spread و slippage را لحاظ کند. فرمول و rounding باید instrument-aware باشد. خروجی risk ابزار تصمیم‌یار است مگر آنکه execution authority صریحاً جداگانه فعال شده باشد.

## outcome attribution
هر signal یک identity و decision timestamp دارد. outcome window، exit reason، realized result، MAE/MFE و شرایط بازار ثبت می‌شود. attribution باید به engine/version، feature set، model version و dataset revision برگردد.

## calibration و drift
دقت خام کافی نیست. calibration، precision/recall در صورت کاربرد، Brier-like measures، distribution shift، feature drift، outcome drift و latency drift باید با baseline مقایسه شوند. thresholdهای promotion باید از قبل تعریف شوند.

## backtest
Backtest فقط وقتی معتبر است که PIT، transaction cost، slippage، spread، market session، missing data و execution assumptions مشخص باشند. نتیجه باید قابل replay و export باشد و نباید با future leakage آلوده شود.
