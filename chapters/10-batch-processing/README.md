# فصل ۱۰: `Batch Processing`

## Batch Processing

`Batch processing` یک dataset محدود یا انباشته را به‌صورت job اجرا می‌کند. این مدل برای report، ساخت index، آموزش model یا تولید `derived data` مناسب است؛ حتی وقتی نتیجه با تأخیر آماده شود.

## هدف فصل

فصل از ابزارهای Unix و log analysis شروع می‌کند، سپس `MapReduce`، join، فایل‌سیستم توزیع‌شده و نسل‌های بعدی APIهای `batch processing` را توضیح می‌دهد.

## نقشهٔ مطالب

- Unix pipeline و تحلیل سادهٔ log
- MapReduce و distributed filesystem
- اجرای job، join سمت reduce و join سمت map
- خروجی workflow و مقایسه با distributed database
- materialized intermediate state و پردازش گراف

## خلاصهٔ زمینه‌محور

### Unix و pipeline

ابزارهای کوچک Unix از ورودی متنی می‌خوانند، یک کار مشخص انجام می‌دهند و خروجی را به ابزار بعدی می‌سپارند. این composability برای تحلیل log مفید است: filter، parse، group و count هر کدام مرحله‌ای قابل‌آزمون می‌شوند. محدودیت این روش آن است که دادهٔ بزرگ روی یک ماشین یا یک فایل‌سیستم معمولی جا نمی‌شود و recovery و parallelism باید جدا طراحی شوند.

### MapReduce

در MapReduce، تابع map رکوردها را به جفت‌های کلید-مقدار تبدیل می‌کند. مرحلهٔ shuffle کلیدهای مشابه را کنار هم می‌آورد و reduce آن گروه‌ها را خلاصه می‌کند. distributed filesystem فایل ورودی و خروجی را روی nodeها نگه می‌دارد و job scheduler تلاش می‌کند محاسبه نزدیک داده اجرا شود.

محاسبهٔ موازی فقط تقسیم تابع نیست. partition، تکرار task شکست‌خورده، کندترین worker، حجم shuffle و تعداد فایل‌های خروجی بر زمان و هزینه اثر دارند. خروجی هر مرحله باید نام‌گذاری، atomic و قابل‌تشخیص از اجرای ناقص باشد.

### join و grouping

در reduce-side join، هر دو dataset بر اساس کلید به reduce می‌روند. این روش عمومی است، اما shuffle بزرگی ایجاد می‌کند. در map-side join، اگر یکی از datasetها کوچک یا از قبل بر اساس کلید مرتب و partition شده باشد، می‌توان آن را در حافظه یا lookup محلی map کرد و هزینهٔ شبکه را کم کرد. انتخاب به اندازهٔ داده، skew و ترتیب فایل‌ها وابسته است.

### `Workflow` output

خروجی batch می‌تواند report نهایی، index، فایل partition شده یا دادهٔ آماده برای سرویس باشد. اگر خروجی به‌صورت derived data ساخته می‌شود، باید بتوان آن را از source دوباره تولید کرد. این ویژگی امکان اصلاح bug، تغییر منطق و backfill را فراهم می‌کند. side effectهای غیرقابل‌بازسازی در میان job، retry را خطرناک می‌کنند.

### `Hadoop` و `database`

یک distributed database query را با schema، index، optimizer و transaction semantics مدیریت می‌کند؛ MapReduce workflow را با مرحله‌های صریح روی فایل‌ها اجرا می‌کند. این دو دسته هم‌پوشانی دارند، اما سؤال‌های متفاوتی را ساده می‌کنند. سیستم‌های جدید با dataflow engine، execution plan و API سطح بالاتر فاصلهٔ syntax را کم کرده‌اند.

### فراتر از `MapReduce`

materializing intermediate state اجازه می‌دهد job طولانی پس از یک مرحله ادامه پیدا کند و دادهٔ مشترک چند query یک‌بار محاسبه شود. در پردازش گراف، iteration و همگام‌سازی مرزهای superstep اهمیت دارد. APIهای declarative می‌توانند join و grouping را از کد سطح پایین جدا کنند، ولی هنوز باید دربارهٔ partition، skew و failure فکر کرد.

### مثال مستقل: گزارش latency سرویس

لاگ هر درخواست شامل شناسهٔ endpoint، زمان پاسخ و status است. یک pipeline می‌تواند ابتدا رکوردهای ناقص را حذف و زمان را bucket کند، سپس بر اساس endpoint و bucket گروه‌بندی کند و در پایان percentileها و نرخ خطا را تولید کند. اگر job از روی log خام قابل‌تکرار باشد، تغییر bucket یا اصلاح parser بدون دستکاری دستی report ممکن می‌شود.

## نکته‌های کلیدی

1. pipeline مرحله‌ای، امکان فهم و retry را بیشتر می‌کند.
2. shuffle و skew اغلب گلوگاه اصلی MapReduce هستند.
3. خروجی derived باید قابل‌بازسازی و قابل‌تشخیص از اجرای ناقص باشد.
4. batch و database جایگزین مطلق یکدیگر نیستند.

## ارتباط با فصل‌های دیگر

- [فصل ۳: `Storage` و `Retrieval`](../03-storage-retrieval/README.md)
- [فصل ۶: `Partitioning` و `Sharding`](../06-partitioning/README.md)
- [فصل ۱۱: `Stream Processing`](../11-stream-processing/README.md)

## الگوی `Batch` pipeline

```mermaid
flowchart LR
    I[ورودی خام] --> V[اعتبارسنجی]
    V --> N[normalization]
    N --> G[grouping یا join]
    G --> A[aggregation]
    A --> O[خروجی نسخه‌دار]
    O --> P[atomic publish]
```

هر مرحله باید ورودی و خروجی قابل‌شمارش داشته باشد. خروجی با نام موقت ساخته می‌شود و تنها پس از کامل‌شدن به نام نهایی منتقل می‌گردد؛ این کار باعث می‌شود consumer فایل ناقص را نبیند.

## انتخاب روش join

| وضعیت داده | روش مناسب‌تر | کنترل لازم |
| --- | --- | --- |
| یک طرف کوچک و ثابت | map-side با lookup محلی | حافظه و تازگی lookup |
| هر دو طرف بزرگ | reduce-side join | shuffle، skew و partition |
| هر دو از قبل هم‌تراز | merge join | قرارداد sort و partition |
| query تعاملی تکراری | materialized view یا warehouse | refresh و lineage |

## مقابله با skew

کلیدهای پرتکرار باعث می‌شوند یک reducer بسیار بیشتر از بقیه کار کند. برای تشخیص، histogram کلیدها و زمان هر task را ثبت کنید. راه‌حل می‌تواند splitکردن کلید داغ، pre-aggregation در map، نمونه‌برداری یا مسیر جدا برای tenant بزرگ باشد. صرفاً افزودن worker مشکل یک کلید منفرد را حل نمی‌کند.

## سناریوی طراحی: محاسبهٔ هزینهٔ ارسال

ورودی شامل سفارش‌ها، منطقهٔ مقصد و جدول نرخ روزانه است. ابتدا رکوردهای نامعتبر جدا می‌شوند، نرخ کوچک در cache worker قرار می‌گیرد، هزینه بر اساس zone محاسبه می‌شود و نتیجه با نسخهٔ نرخ ذخیره می‌گردد. اگر نرخ اصلاح شود، اجرای دوبارهٔ بازهٔ زمانی باید فقط view هزینه را عوض کند و source سفارش‌ها را دست‌کاری نکند.

## چک‌لیست job

- [ ] ورودی immutable یا snapshot شده است.
- [ ] retry یک task خروجی duplicate تولید نمی‌کند.
- [ ] دادهٔ ورودی، نسخهٔ کد و پارامترها ثبت شده‌اند.
- [ ] skew و کندترین task اندازه‌گیری می‌شوند.
- [ ] خروجی قابل‌بازسازی و انتشار آن atomic است.

## تمرین‌های مرور

1. برای join دو dataset بزرگ، هزینهٔ شبکه و محل shuffle را تخمین بزنید.
2. یک روش تشخیص اجرای ناقص job طراحی کنید.
3. توضیح دهید چرا خروجی derived باید از source دوباره ساخته شود.

## تعریف مستقل اصطلاحات

### `batch processing`

**چیست؟** پردازش یک dataset موجود یا یک بازهٔ مشخص از داده، معمولاً به‌صورت job.

**مثال:** محاسبهٔ گزارش فروش کل ماه گذشته.

### `MapReduce`

**چیست؟** الگویی که map داده را تبدیل می‌کند، shuffle کلیدهای مشترک را کنار هم می‌آورد و reduce هر گروه را خلاصه می‌کند.

**اشتباه رایج:** MapReduce فقط «چند worker» نیست؛ جابه‌جایی داده، retry task و skew بخش مهم آن‌اند.

### `shuffle`

**چیست؟** مرحله‌ای که خروجی map بر اساس key بین workerها جابه‌جا و گروه‌بندی می‌شود.

**خطر:** اگر یک key بسیار پرتکرار باشد، یک worker می‌تواند گلوگاه کل job شود.

### `reduce-side join` و `map-side join`

در `reduce-side join` هر دو dataset بر اساس key به مرحلهٔ reduce می‌روند؛ عمومی اما پرهزینه‌تر است. در `map-side join` بخشی از داده از قبل local یا کوچک است و map بدون shuffle بزرگ join را انجام می‌دهد.

### `backfill`

**چیست؟** اجرای دوبارهٔ منطق روی دادهٔ قدیمی برای پرکردن یا اصلاح یک view.

**مثال:** parser قیمت اشتباه بوده و باید گزارش سه ماه گذشته دوباره تولید شود.

### `materialized view`

**چیست؟** نتیجهٔ ذخیره‌شدهٔ یک query یا aggregation برای read سریع‌تر.

**اشتباه رایج:** materialized view منبع حقیقت نیست؛ باید freshness، refresh و روش rebuild داشته باشد.
