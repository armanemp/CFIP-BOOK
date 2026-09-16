# ۹. Smart Search و Research Intelligence Fabric

جست‌وجوی هوشمند باید evidence-first باشد. مسیر مرجع: Query → Policy → Planner → Expansion → Retrieval → Fusion → Reranker → Evidence Assembly → Elyrava reasoning → Citation Verification → Answer.

Retrieval می‌تواند ترکیبی از lexical/BM25 و vector باشد. Fusion نباید relevance را با truth اشتباه بگیرد. Reranker فقط ترتیب evidence را بهتر می‌کند و جای verification را نمی‌گیرد.

## Research Fabric
Ingestion → normalization → extraction → classification → deduplication → provenance → indexing → retrieval → evidence graph → synthesis → citation check → feedback/evaluation.

محتوای وب، issue، README، PDF و کد خارجی untrusted است. آن‌ها فقط data هستند و نباید به‌عنوان instruction به agent منتقل شوند. citation باید به منبع و snapshot/زمان تحقیق متصل باشد. freshness gate برای اطلاعاتی که تغییر می‌کنند الزامی است.

## research record
هر تحقیق باید query، scope، sources، retrieved_at، source version، extracted claims، citations، trust classification، tool actions، model/version و نتیجه verification را نگه دارد. نتیجه research بدون provenance نباید وارد تصمیم حساس شود.

## GitHub research
جست‌وجو باید capability-based باشد: «چه مسئله‌ای را می‌خواهیم حل کنیم؟» سپس repository candidates با license، health، security، API، performance و fit ارزیابی می‌شوند. پروژه‌ای که فقط یک demo است نباید به‌عنوان زیرساخت production ثبت شود.
