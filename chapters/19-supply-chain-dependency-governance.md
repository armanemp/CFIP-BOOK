# ۱۹. امنیت supply-chain و dependency governance

هر dependency باید مالک، نسخه، license، reason، transitive risk و جایگزین/exit strategy داشته باشد. lockfile و reproducible build برای جلوگیری از drift ضروری‌اند.

Security scanning باید source، container و dependency را پوشش دهد. CVE به تنهایی معیار تصمیم نیست؛ exploitability، exposure و compensating control نیز ثبت می‌شود.

پروژه‌های GitHub باید commit/release provenance و maintainer health داشته باشند. کپی‌کردن کد بدون بررسی license ممنوع است. generated code نیز dependency و license خودش را پنهان نمی‌کند.

در runtime، permissions حداقلی و filesystem/network محدود برای workerهای پرریسک و sandboxهای agentی اعمال می‌شود.
