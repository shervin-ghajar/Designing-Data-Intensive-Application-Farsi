# پیشگفتار

## `Preface`

اگر در سال‌های اخیر در مهندسی نرم‌افزار، به‌ویژه در سامانه‌های server-side و backend، کار کرده باشید، احتمالاً با انبوهی از واژه‌های مد روز دربارهٔ ذخیره‌سازی و پردازش data روبه‌رو شده‌اید: `NoSQL`، `Big Data`، `web-scale`، `sharding`، `eventual consistency`، `ACID`، `CAP theorem`، cloud services، `MapReduce` و real-time.

در دههٔ گذشته، در databaseها، distributed systems و روش ساخت applicationها پیشرفت‌های جالبی رخ داده است. شرکت‌های اینترنتی مانند Google، Yahoo!، Amazon، Facebook، LinkedIn، Microsoft و Twitter با حجم بسیار بزرگی از data و traffic روبه‌رو شده‌اند و ابزارهای تازه‌ای برای مدیریت این scale ساخته‌اند. کسب‌وکارها نیز باید فرضیه‌ها را ارزان آزمایش کنند، سریع به insightهای بازار پاسخ دهند و data modelهای انعطاف‌پذیر داشته باشند.

نرم‌افزار آزاد و open source موفق شده است؛ processorهای چند‌هسته‌ای و networkهای سریع‌تر، parallelism را مهم‌تر کرده‌اند؛ و infrastructure as a service یا `IaaS` مانند Amazon Web Services به تیم‌های کوچک اجازه می‌دهد systemهایی بسازند که روی ماشین‌ها و regionهای مختلف پخش شده‌اند. از طرف دیگر، availability بالا برای بسیاری از serviceها به یک انتظار معمول تبدیل شده است و downtime طولانی دیگر به‌سادگی پذیرفته نمی‌شود.

این پیشرفت‌ها مرز کاری را که با `data-intensive application`ها ممکن است جابه‌جا کرده‌اند. برنامه‌ای `data-intensive` است اگر مسئلهٔ اصلی آن data باشد: مقدار data، پیچیدگی data یا سرعت تغییر آن. در برنامهٔ `compute-intensive`، معمولاً چرخه‌های CPU گلوگاه اصلی‌اند.

ابزارهایی که به برنامه‌های `data-intensive` برای ذخیره و پردازش data کمک می‌کنند، به‌سرعت تغییر کرده‌اند. انواع جدید database، که معمولاً با نام `NoSQL` شناخته می‌شوند، مهم‌اند؛ اما message queue، cache، search index، `batch processing` و `stream processing` نیز به همان اندازه در بسیاری از applicationها نقش دارند. یک application معمولاً ترکیبی از چند ابزار است.

## فراتر از واژه‌های مد روز

پرشدن این حوزه از buzzwordها نشانهٔ امکان‌های جدید است، اما software engineer و architect باید از این واژه‌ها عمیق‌تر بروند و technologyها و trade-offهای آن‌ها را دقیق بفهمند. پشت تغییرهای سریع technology، اصول ماندگاری وجود دارد که مستقل از نسخهٔ یک ابزار خاص همچنان درست‌اند. اگر این اصول را بفهمید، می‌توانید تشخیص دهید هر ابزار کجا مناسب است، چطور از آن درست استفاده کنید و از چه دام‌هایی دور بمانید.

هدف کتاب این است که به شما کمک کند در چشم‌انداز متنوع و دائماً در حال تغییر فناوری‌های ذخیره و پردازش data راه خود را پیدا کنید. کتاب راهنمای کار با یک ابزار خاص یا textbookای پر از نظریهٔ خشک نیست. در عوض، نمونه‌هایی از data systemهای موفق را بررسی می‌کند؛ systemهایی که پایهٔ بسیاری از applicationهای محبوب‌اند و هر روز در production باید نیازهای scalability، performance و reliability را برآورده کنند.

درون این systemها، algorithmهای اصلی و trade-offهایشان بررسی می‌شود. در این مسیر فقط نمی‌پرسیم system چگونه کار می‌کند؛ می‌پرسیم چرا این‌گونه کار می‌کند و هنگام طراحی چه سؤال‌هایی باید بپرسیم.

پس از خواندن کتاب، آمادگی خوبی خواهید داشت تا تصمیم بگیرید کدام technology برای کدام هدف مناسب است و چطور چند ابزار را برای ساختن پایهٔ یک application architecture خوب کنار هم قرار دهید. قرار نیست بتوانید یک storage engine را از صفر بسازید؛ خوشبختانه در بیشتر مواقع چنین کاری لازم نیست. اما درک خوبی از اتفاق‌هایی که زیر پوستهٔ system می‌افتند پیدا می‌کنید و می‌توانید رفتار system را تحلیل، تصمیم طراحی را ارزیابی و مشکل‌های احتمالی را پیدا کنید.

## این کتاب برای چه کسانی است؟

اگر applicationهایی می‌سازید که برای ذخیره یا پردازش data به server یا backend نیاز دارند و از Internet استفاده می‌کنند، این کتاب برای شماست. این موضوع شامل web application، mobile application و sensorهای متصل به Internet می‌شود.

کتاب برای software engineerها، software architectها و مدیران فنی‌ای نوشته شده است که از codeزدن لذت می‌برند. کتاب به‌خصوص زمانی مفید است که باید دربارهٔ architecture system تصمیم بگیرید؛ مثلاً ابزار مناسب برای یک مسئله را انتخاب کنید و بفهمید چطور باید آن را به کار بگیرید. حتی اگر اختیار انتخاب ابزار را نداشته باشید، کتاب کمک می‌کند قدرت‌ها و ضعف‌های آن را بهتر بفهمید.

بهتر است تجربه‌ای در ساخت web application یا network service داشته باشید و با `relational database` و `SQL` آشنا باشید. آشنایی با databaseهای non-relational و ابزارهای data امتیاز محسوب می‌شود، اما ضروری نیست. دانستن کلیات protocolهای معمول network مانند `TCP` و `HTTP` نیز مفید است. زبان programming یا framework انتخابی شما اهمیتی ندارد.

این کتاب برای کسی مناسب است که می‌خواهد data systemها را برای میلیون‌ها user scalable کند، applicationهای highly available و operationally robust بسازد، systemها را در بلندمدت maintainable نگه دارد یا بفهمد درون websiteها و online serviceهای بزرگ چه می‌گذرد.

گاهی گفته می‌شود: «شما Google یا Amazon نیستید؛ نگران scale نباشید و فقط از یک relational database استفاده کنید.» این حرف بخشی از حقیقت را دارد: ساختن چیزی برای scaleای که به آن نیاز ندارید، تلاش هدررفته و گاهی premature optimization است. بااین‌حال، انتخاب ابزار مناسب مهم است و relational databaseها پاسخ نهایی همهٔ مسئله‌های data نیستند.

## دامنهٔ کتاب

کتاب دستورالعمل نصب یا استفاده از packageها و APIهای مشخص را ارائه نمی‌کند؛ برای این کارها مستندات فراوانی وجود دارد. تمرکز بر اصول و trade-offهای بنیادی data systemها و تصمیم‌های طراحی productهای گوناگون است.

تمرکز اصلی بر architecture data systemها و روش یکپارچه‌کردن آن‌ها در `data-intensive application`هاست. deployment، operations، security و management حوزه‌هایی پیچیده‌اند و این کتاب آن‌ها را فقط در حدی مطرح می‌کند که به معماری data مربوط باشند.

عبارت `Big Data` آن‌قدر زیاد و بدون تعریف دقیق استفاده شده که در گفت‌وگوی جدی مهندسی چندان مفید نیست؛ به‌جای آن از عبارت‌های روشن‌تری مانند single-node در برابر distributed system یا online/interactive در برابر offline/`batch processing` استفاده می‌شود. کتاب گرایش زیادی به نرم‌افزار آزاد و open source یا `FOSS` دارد، چون خواندن، تغییر دادن و اجراکردن source code راه خوبی برای فهمیدن کارکرد system است؛ بااین‌حال، softwareهای proprietary نیز هر جا لازم باشد بررسی می‌شوند.

## نقشهٔ کتاب

کتاب در سه بخش تنظیم شده است:

1. **بخش اول** دربارهٔ ایده‌های بنیادی طراحی `data-intensive application`هاست. فصل ۱ `reliability`، `scalability` و `maintainability` را بررسی می‌کند. فصل ۲ data modelها و query languageها را مقایسه می‌کند. فصل ۳ به storage engineها می‌پردازد و فصل ۴ قالب‌های `encoding` یا serialization data و تکامل schemaها را بررسی می‌کند.
2. **بخش دوم** از data ذخیره‌شده روی یک ماشین به dataای می‌رود که میان چند ماشین توزیع شده است. `replication`، `partitioning` یا `sharding` و `transaction`ها بررسی می‌شوند و بعد کتاب به مسئله‌های distributed systemها و معنای consistency و consensus می‌پردازد.
3. **بخش سوم** دربارهٔ systemهایی است که datasetها را از datasetهای دیگر می‌سازند. `Derived data` در systemهای ناهمگون با ترکیب database، cache، index و ابزارهای دیگر شکل می‌گیرد. فصل ۱۰ `batch processing`، فصل ۱۱ `stream processing` و فصل ۱۲ معماری applicationهای reliable، scalable و maintainable در آینده را بررسی می‌کند.

## References و مطالعهٔ بیشتر

بخش بزرگی از مطالب کتاب پیش‌تر در conference presentationها، research paperها، blogها، code، bug trackerها، mailing listها و تجربه‌های مهندسی بیان شده‌اند. کتاب مهم‌ترین ایده‌ها را از منابع مختلف جمع می‌کند و در پایان هر فصل به منابع اصلی اشاره می‌کند. بیشتر این منابع برای مطالعهٔ عمیق‌تر به‌صورت آزاد در Internet در دسترس‌اند.

در این branch، بخش‌های تبلیغاتی ناشر، اطلاعات تماس و `Index` که برای یادگیری مفهوم‌های فنی لازم نیستند وارد ترجمه نشده‌اند.
