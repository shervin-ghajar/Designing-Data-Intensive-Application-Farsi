# راهنمای یکدستی اصطلاحات

این جدول canonical vocabulary پروژه است. واژهٔ ستون اول ترجمه نمی‌شود؛ ستون دوم فقط توضیح سادهٔ فارسی است. اگر خواننده تازه‌کار است، ابتدا واژه را بیاورید و بعد معنی آن را توضیح دهید.

| Canonical term | توضیح ساده، نه ترجمهٔ جایگزین |
| --- | --- |
| `data-intensive application` | برنامه‌ای که حجم، سرعت تغییر یا پیچیدگی داده مسئلهٔ اصلی آن است. |
| `reliability` | سامانه در برابر خرابی هم رفتار درست خود را حفظ کند. |
| `scalability` | با رشد load، روش قابل‌قبولی برای افزایش ظرفیت داشته باشیم. |
| `maintainability` | فهمیدن، اجراکردن و تغییر سامانه در طول زمان آسان بماند. |
| `operability` | اجرا، پایش، عیب‌یابی و تعمیر روزمره قابل‌مدیریت باشد. |
| `simplicity` | رفتار system بدون پیچیدگی تصادفی قابل‌فهم بماند. |
| `evolvability` | schema، API و اجزا با تغییر نیازها قابل‌تکامل باشند. |
| `fault` | یک component از spec خود منحرف شود. |
| `failure` | کل سرویس نتیجهٔ مورد انتظار را به کاربر ندهد. |
| `resilience` | سامانه بتواند از fault ادامه دهد یا recovery کند. |
| `latency` | مدت‌زمان رسیدن پاسخ. |
| `throughput` | مقدار کاری که در واحد زمان انجام می‌شود. |
| `load` | فشاری که request، data یا connection روی سیستم می‌آورد. |
| `schema` | قرارداد fieldها، typeها و معنی data. |
| `query` | درخواست خواندن، ترکیب یا تغییر data. |
| `index` | ساختار کمکی برای پیدا کردن data سریع‌تر. |
| `transaction` | چند operation که با یک قرارداد atomic اجرا می‌شوند. |
| `atomicity` | یا همهٔ operationهای یک transaction اثر می‌کنند یا هیچ‌کدام اثر نهایی ندارند. |
| `isolation` | میزان جدا دیده‌شدن transactionهای هم‌زمان. |
| `serializability` | نتیجه مثل اجرای معتبر transactionها به‌صورت ترتیبی باشد. |
| `snapshot isolation` | transaction یک تصویر ثابت از data را ببیند. |
| `replication` | نگه‌داشتن چند copy از data روی چند node. |
| `leader` / `follower` | leader write را ترتیب می‌دهد و follower تغییرها را دنبال می‌کند. |
| `multi-leader` | چند node هم‌زمان می‌توانند write بپذیرند. |
| `leaderless` | write به چند replica فرستاده می‌شود و leader ثابت وجود ندارد. |
| `replication lag` | فاصلهٔ نسخهٔ یک replica با جدیدترین تغییر. |
| `quorum` | حداقل تعداد پاسخ لازم برای معتبر دانستن operation. |
| `partition` | بخشی از dataset با مالکیت یا پردازش مشخص. |
| `partitioning` | تقسیم dataset بین partitionها. |
| `sharding` | نام رایج تقسیم افقی data بین shardها. |
| `rebalancing` | جابه‌جایی مالکیت partitionها بعد از تغییر node یا load. |
| `normalization` | کم‌کردن تکرار data و نگه‌داشتن source در یک محل معتبر. |
| `denormalization` | تکرار کنترل‌شدهٔ data برای سریع‌ترشدن read. |
| `hotspot` | key یا partitionای که بار نامتناسب می‌گیرد. |
| `consistency` | قراردادی دربارهٔ نسخه‌ای که read می‌بیند. |
| `eventual consistency` | replicaها اگر write جدیدی نیاید، در نهایت همگرا می‌شوند. |
| `linearizability` | operationها انگار روی یک copy و در یک ترتیب واقعی اجرا می‌شوند. |
| `consensus` | چند node روی یک decision یا order توافق می‌کنند. |
| `ordering` | قراردادی دربارهٔ ترتیب دیده‌شدن eventها. |
| `causality` | رابطهٔ علت و معلول بین eventها. |
| `distributed system` | چند process یا node که از راه network با هم کار می‌کنند. |
| `partial failure` | بخشی از system خراب است و بقیه هنوز کار می‌کنند. |
| `clock skew` | اختلاف ساعت nodeها با یکدیگر یا زمان واقعی. |
| `Byzantine fault` | component ممکن است رفتار دلخواه یا دروغ‌گو داشته باشد. |
| `encoding` | تبدیل object به text یا byte برای storage یا انتقال. |
| `schema evolution` | تغییر schema در حالی که data یا consumer قدیمی هنوز وجود دارد. |
| `message passing` | ارتباط processها با send و receive کردن message. |
| `batch processing` | پردازش dataset موجود در قالب job. |
| `stream processing` | پردازش پیوستهٔ eventهایی که وارد می‌شوند. |
| `event stream` | دنباله‌ای از eventها که معمولاً قابل replay است. |
| `log` | دنبالهٔ مرتب و ماندگار از تغییرها یا eventها. |
| `change data capture` | تبدیل تغییرهای database به event. |
| `event sourcing` | نگه‌داشتن eventها به‌عنوان source اصلی و ساخت state با replay. |
| `materialized view` | نتیجهٔ ذخیره‌شدهٔ یک محاسبه برای read سریع‌تر. |
| `data warehouse` | storage تحلیلی برای scan و aggregation بزرگ. |
| `column-oriented storage` | کنار هم نگه‌داشتن valueهای یک column برای analytics. |
| `OLTP` | Online Transaction Processing؛ workload عملیاتی با read/writeهای کوچک و latency پایین. |
| `OLAP` | Online Analytical Processing؛ workload تحلیلی با scan و aggregation بزرگ. |
| `compatibility` | نسخهٔ جدید و قدیمی بتوانند طبق قرارداد مشترک data یا message را مصرف کنند. |
| `dataflow` | مسیر حرکت data از source تا viewها و consumerها. |
| `end-to-end argument` | تضمین نهایی باید در دو سر operation هم بررسی شود. |

اصطلاحات فنی تثبیت‌شده مانند `ACID`، `CAP`، `REST`، `RPC`، `SQL`، `NoSQL`، `MapReduce`، `SSTable`، `LSM-tree` و `B-tree` به همان شکل اصلی باقی می‌مانند.

## واژه‌های ترجمه‌نشده و تعریف ساده

این واژه‌ها عمداً ترجمه نمی‌شوند، چون معادل فارسی آن‌ها ممکن است معنی فنی را عوض کند یا با یک مفهوم دیگر اشتباه شود. هر کدام باید در فصل مربوط به‌صورت جداگانه تعریف شوند.

| واژه | تعریف بسیار ساده |
| --- | --- |
| `idempotency` | اگر یک درخواست چندبار اجرا شود، اثر نهایی آن مثل یک‌بار اجراشدن باقی بماند. |
| `document` | یک بستهٔ مستقل از داده که معمولاً با هم خوانده می‌شود. |
| `relational` | مدلی که داده را در جدول‌ها و رابطه‌های مشخص بین آن‌ها نگه می‌دارد. |
| `outbox` | جدولی کنار تغییر اصلی که نیت ارسال event را در همان transaction ثبت می‌کند. |
| `inbox` | محلی برای ثبت پیام‌های دیده‌شده تا consumer آن‌ها را دوباره اعمال نکند. |
| `saga` | چند مرحلهٔ مستقل با actionهای جبرانی، به‌جای یک transaction سراسری. |
| `retry` | تلاش دوباره پس از خطای موقت، با حد و قانون مشخص. |
| `timeout` | مهلتی که پس از آن پاسخ را دیرشده فرض می‌کنیم؛ نه اثبات قطعی شکست. |
| `backoff` | فاصلهٔ افزایشی بین retryها برای کم‌کردن فشار. |
| `jitter` | تغییر تصادفی کوچک در زمان retry برای جلوگیری از هم‌زمانی همهٔ clientها. |
| `CDC` | تبدیل تغییرهای database به event قابل‌مصرف برای سیستم‌های دیگر. |
| `event sourcing` | نگه‌داری eventهای تغییر به‌عنوان منبع اصلی و ساخت state از روی آن‌ها. |

قالب کامل تعریف هر واژه در [STYLE_GUIDE.md](./STYLE_GUIDE.md) آمده است.
