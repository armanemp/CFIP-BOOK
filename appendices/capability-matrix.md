# ماتریس جامع قابلیت‌ها

| حوزه | قابلیت | مالک مفهومی | داده اصلی | شواهد لازم | gate بحرانی |
|---|---|---|---|---|---|
| بازار | ingestion/normalization | Market Data | observations | adapter + fixtures | D2,D3,D9 |
| بازار | instrument identity | Instruments | canonical instruments | mapping tests | D3,D4 |
| ساختار | FVG | Structure | zones/lifecycle | parity + replay | D4,D7 |
| ساختار | Order Block/MTF | Structure | zones/relations | fixtures | D4,D7 |
| تحلیل | indicators/features | Analytics | feature sets | numerical tests | D4,D7 |
| تحلیل | signals/consensus | Intelligence | signal/evidence | conflict tests | D4,D7 |
| ریسک | position sizing | Risk | account/constraints | formula fixtures | D7 |
| شبیه‌سازی | backtest/replay | Replay | PIT datasets | no-leakage tests | D3,D7 |
| پژوهش | search/research | Research | evidence | citation/freshness | D7,D9 |
| هوش | Elyrava | Platform Intelligence | actions/evidence | policy + sandbox | D8,D10 |
| محصول | terminal | Experience | UI state | E2E/a11y | D6,D7 |
| حساب | identity/access | Identity | users/sessions | security tests | D1,D7 |
| درآمد | billing/entitlement | Commerce | ledger/subscription | reconciliation | D2,D7,D10 |
| عملیات | observability | Operations | telemetry | SLO evidence | D10 |

هر ردیف باید lifecycle و evidence state جداگانه داشته باشد. خالی‌بودن یکی از آن‌ها یعنی capability بسته نشده است.
