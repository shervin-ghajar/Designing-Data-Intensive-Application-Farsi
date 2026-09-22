# خلاصهٔ فشردهٔ کتاب

این فایل یک راهنمای مستقل برای یادگیری سریع ۱۲ فصل است. هر بخش، ایدهٔ مرکزی، مفاهیم ضروری و قواعد تصمیم‌گیری همان فصل را جمع می‌کند. برای دقت فنی، اصطلاحات تخصصی به شکل اصلی آمده‌اند.

## فصل ۱: <span dir="ltr">Reliability, Scalability, Maintainability</span>

### ایدهٔ مرکزی

یک `data-intensive application` فقط نباید جواب درست بدهد؛ باید در برابر خرابی، افزایش load و تغییرات آینده هم قابل‌اعتماد بماند. این سه هدف به هم مرتبط‌اند، اما یکی نیستند:

- &rlm;`Reliability`: سیستم با وجود `fault`های سخت‌افزاری، نرم‌افزاری یا انسانی، رفتار درست و قابل‌پیش‌بینی داشته باشد.
- &rlm;`Scalability`: با افزایش data، traffic یا تعداد userها، بتوان ظرفیت را افزایش داد و performance را در محدودهٔ قابل‌قبول نگه داشت.
- &rlm;`Maintainability`: فهمیدن، operation، تغییر دادن و توسعه‌دادن سیستم برای تیم آسان بماند.

### نکات کلیدی

&rlm;`Fault` علت بالقوهٔ مشکل است و `failure` خراب‌شدن observable سرویس. طراحی خوب همهٔ faultها را حذف نمی‌کند؛ آن‌ها را محدود، آشکار و قابل‌بازیابی می‌کند. retry، replication، timeout، validation و monitoring ابزارهای مقابله با fault هستند، اما هرکدام می‌توانند هزینه و failure جدید بسازند.

برای سنجش `Scalability` ابتدا load را با عدد توصیف کنید: request در ثانیه، نسبت read به write، اندازهٔ response یا تعداد userهای هم‌زمان. سپس performance را با latency و مخصوصاً percentileهای بالاتر مانند p95 و p99 بسنجید؛ average می‌تواند tail latency را پنهان کند. scale کردن فقط اضافه‌کردن machine نیست؛ باید bottleneck، partition، cache، queue و الگوی access را شناخت.

&rlm;`Maintainability` سه بُعد دارد: `Operability` برای اجرای سالم و مشاهدهٔ وضعیت، `Simplicity` برای کم‌کردن complexity غیرضروری، و `Evolvability` برای تغییر امن در آینده. abstraction خوب جزئیات را پنهان می‌کند، اما abstraction بد پیچیدگی را فقط جابه‌جا می‌کند.

### قاعدهٔ عملی

قبل از انتخاب technology، requirementها و failure modeها را بنویسید، load و latency را اندازه بگیرید، و هر guarantee را به هزینه‌اش وصل کنید. معماری خوب از چند component ساده ساخته می‌شود، به شرطی که interface، ownership و guarantee هر component روشن باشد.

## فصل ۲: <span dir="ltr">Data Models and Query Languages</span>

### ایدهٔ مرکزی

انتخاب `data model` فقط انتخاب شکل ذخیره‌سازی نیست؛ این انتخاب تعیین می‌کند مسئله را چگونه ببینیم، چه queryهایی طبیعی باشند و کدام تغییرات در آینده ارزان یا گران شوند. هر layer داده را با model مناسب خودش نمایش می‌دهد و complexity layer پایین‌تر را پنهان می‌کند.

### نکات کلیدی

- &rlm;`Relational` model برای داده‌های ساختاریافته، رابطه‌های صریح، constraint و queryهای ترکیبی مناسب است. `normalization` یک حقیقت را در یک محل نگه می‌دارد و update را امن‌تر می‌کند؛ هزینه‌اش join و چند read است.
- &rlm;`Document` model دادهٔ نزدیک به هم را در یک document نگه می‌دارد. locality خواندن و schema انعطاف‌پذیر مزیت آن است؛ اما رابطه‌های many-to-many، joinهای پیچیده و duplicate شدن داده می‌تواند مشکل‌ساز شود. `denormalization` باید بر اساس access pattern و با برنامهٔ update انجام شود.
- &rlm;`Graph` model برای مسئله‌هایی مناسب است که رابطه‌ها خودشان بخش اصلی داده‌اند و هر vertex می‌تواند با vertexهای زیادی ارتباط داشته باشد. property graph، `SPARQL` و `Datalog` شکل‌های مختلف query این فضا هستند.

زبان `declarative` مانند SQL می‌گوید چه داده‌ای می‌خواهیم، نه دقیقاً چگونه آن را پیدا کنیم؛ در نتیجه query optimizer می‌تواند plan مناسب انتخاب کند. زبان imperative کنترل بیشتری می‌دهد، اما application را به جزئیات اجرا وابسته می‌کند. هیچ modelی برای همهٔ workloadها بهترین نیست و می‌توان بعضی modelها را با model دیگر شبیه‌سازی کرد، ولی معمولاً با پیچیدگی بیشتر.

### قاعدهٔ عملی

ابتدا entityها، relationshipها، invariantها و queryهای واقعی را فهرست کنید؛ سپس model را انتخاب کنید. اگر بیشتر queryها یک object و اجزای نزدیک آن را می‌خوانند، `document` می‌تواند مناسب باشد. اگر join، constraint و رابطه‌های متقابل مهم‌اند، `relational` مناسب‌تر است. اگر مسیر و ارتباط چندمرحله‌ای محور مسئله است، `graph` را بررسی کنید.

## فصل ۳: <span dir="ltr">Storage and Retrieval</span>

### ایدهٔ مرکزی

&rlm;database در اصل دو کار انجام می‌دهد: write را با هزینهٔ مناسب ثبت می‌کند و record موردنیاز را سریع پیدا می‌کند. `Storage engine` بر اساس workload برای این دو کار trade-off می‌سازد؛ بنابراین انتخاب database بدون شناخت الگوی access خطرناک است.

### نکات کلیدی

در workloadهای `OLTP` معمولاً requestهای کوچک و lookup بر اساس key داریم. دو خانوادهٔ اصلی storage engine این‌ها هستند:

- &rlm;`Log-structured`: writeها را append می‌کند و با `compaction` فایل‌ها را مرتب و ادغام می‌کند. `SSTable` و `LSM-tree` نمونه‌های این خانواده‌اند. write sequential و throughput بالا مزیت است؛ compaction، read amplification و write amplification هزینه‌اند.
- &rlm;`Update-in-place`: داده را در pageهای قابل‌تغییر نگه می‌دارد. `B-tree` نمونهٔ اصلی است؛ read و range query قابل‌پیش‌بینی است، اما split page و random write هزینه دارد.

&rlm;`Index` مسیر اضافی برای پیدا کردن داده است و هر index سرعت read را بالا می‌برد، اما write و فضای ذخیره‌سازی را گران‌تر می‌کند. secondary، compound، covering و full-text index برای queryهای متفاوت‌اند. `OLAP` بر خلاف OLTP تعداد query کمتر ولی scan بسیار بزرگ دارد؛ `column-oriented storage`، compression، vectorized processing و sort order برای آن مناسب‌اند. `Materialized view` و `data cube` پاسخ query پرتکرار را از قبل محاسبه می‌کنند، اما freshness و هزینهٔ update دارند.

### قاعدهٔ عملی

اول workload واقعی، اندازهٔ data، نسبت read/write، range query، latency و recovery را اندازه بگیرید؛ بعد engine و index انتخاب کنید. index بیشتر همیشه بهتر نیست. برای analytics، data را از مسیر OLTP جدا و با pipeline به شکل مناسب query تبدیل کنید.

## فصل ۴: <span dir="ltr">Encoding and Evolution</span>

### ایدهٔ مرکزی

دادهٔ داخل memory برای ذخیره یا ارسال باید به byte تبدیل شود (`encoding`) و در مقصد دوباره به object تبدیل شود (`decoding`). این قالب فقط مسئلهٔ حجم و سرعت نیست؛ چون هنگام deployment، نسخه‌های قدیمی و جدید code و data مدتی هم‌زمان وجود دارند.

### نکات کلیدی

قالب‌های متنی مانند `JSON`، `XML` و `CSV` خوانا و فراگیرند، اما دربارهٔ type، number، binary و schema ابهام دارند. `Protocol Buffers`، `Thrift` و `Avro` با schema مشخص، فشرده‌تر و برای evolution قابل‌کنترل‌ترند. در قالب‌های schema-driven، fieldها باید با identifier پایدار شناخته شوند؛ حذف field باید با پشتیبانی از دادهٔ قدیمی و اضافه‌کردن field با default یا optional انجام شود.

- &rlm;`Backward compatibility`: code جدید data نوشته‌شده توسط code قدیمی را بخواند.
- &rlm;`Forward compatibility`: code قدیمی data نوشته‌شده توسط code جدید را تا حد ممکن بخواند و field ناشناخته را نادیده بگیرد.

در `rolling upgrade`، هم‌زیستی versionها عادی است؛ پس تغییر schema را مرحله‌ای و قابل rollback طراحی کنید. مسیر dataflow را هم بشناسید: database، `REST`/`RPC` و message-passing هرکدام writer و reader متفاوت دارند. `RPC` شبیه function call محلی نیست؛ network failure، timeout و retry دارد و operationهای retryشونده باید `idempotency` داشته باشند.

### قاعدهٔ عملی

قبل از تغییر format، جدول سازگاری writer/reader را بسازید. اول field جدید را اضافه و deploy کنید، سپس code را تغییر دهید و فقط زمانی field قدیمی را حذف کنید که همهٔ readerها به‌روز شده باشند. schema را مستند، version را قابل‌ردیابی و migration را قابل‌بازسازی نگه دارید.

## فصل ۵: <span dir="ltr">Replication</span>

### ایدهٔ مرکزی

&rlm;`Replication` یعنی نگه‌داشتن چند copy از یک data روی nodeهای مختلف. هدف آن می‌تواند availability، کاهش latency، تحمل خرابی، افزایش read capacity یا کار در حالت disconnected باشد. مشکل اصلی این است که copyها هم‌زمان و همیشه در دسترس نیستند.

### نکات کلیدی

- &rlm;`Single-leader`: همهٔ writeها به leader می‌روند و followerها changeها را دنبال می‌کنند. ساده‌تر است، اما failover و replication lag دارد.
- &rlm;`Multi-leader`: چند node write می‌پذیرند؛ برای چند datacenter یا collaborative editing مفید است، ولی conflict resolution لازم دارد.
- &rlm;`Leaderless`: client از چند replica می‌خواند و می‌نویسد؛ quorum، read repair و merge برای پیدا کردن مقدار درست به‌کار می‌رود، اما reasoning سخت‌تر است.

در `synchronous replication` تأیید write به replicaهای بیشتری وابسته است؛ دادهٔ تازه‌تر و availability کمتر دارد. `Asynchronous replication` سریع‌تر است، اما lag و احتمال ازبین‌رفتن write تأییدشده هنگام failover را باید پذیرفت. lag فقط مشکل performance نیست و می‌تواند رفتار کاربر را تغییر دهد: `read-after-write` دیدن update خود، `monotonic reads` برنگشتن به گذشته و `consistent prefix reads` دیدن eventهای علّی به ترتیب.

&rlm;conflict را باید با semantics دامنه حل کرد. `Last write wins` ساده است اما ممکن است update معتبر را بی‌صدا حذف کند. timestamp قابل‌اعتماد نیست؛ `version vector` یا merge مبتنی بر domain اطلاعات بیشتری حفظ می‌کند. replication جای backup نیست، چون حذف یا corruption نیز replicate می‌شود.

### قاعدهٔ عملی

برای هر read و write مشخص کنید کدام replica مجاز است، freshness لازم چیست و در failover چه چیزی از دست می‌رود. اگر conflict قابل‌حل نیست، write را به یک leader یا coordination قوی محدود کنید؛ اگر availability مهم‌تر است، merge و conflict resolution را بخشی از domain طراحی کنید.

## فصل ۶: <span dir="ltr">Partitioning</span>

### ایدهٔ مرکزی

وقتی یک node برای data یا load کافی نیست، dataset را به `partition` یا `shard` تقسیم می‌کنیم. هدف فقط پخش‌کردن byteها نیست؛ باید storage و query load هم یکنواخت توزیع شود و `hot spot` ایجاد نشود. partitioning معمولاً همراه replication استفاده می‌شود.

### نکات کلیدی

- &rlm;`Key-range partitioning` keyهای مرتب را به بازه‌ها تقسیم می‌کند. range query خوب است، اما keyهای متوالی، مثل timestamp، می‌توانند همهٔ writeها را به آخرین partition بفرستند.
- &rlm;`Hash partitioning` با hash key توزیع یکنواخت‌تری می‌دهد، اما ترتیب key و range query را از بین می‌برد. `Compound key` می‌تواند بین locality و توزیع تعادل بسازد.
- در `document-partitioned index` write محلی است اما query ممکن است `scatter/gather` شود. در `term-partitioned index` read متمرکزتر است، اما یک write ممکن است چند partition index را تغییر دهد.

هنگام اضافه یا حذف node، `rebalancing` باید data را با کمترین جابه‌جایی و بدون overload توزیع کند. روش `hash mod N` با تغییر N تقریباً همهٔ keyها را جابه‌جا می‌کند. partitionهای ثابتِ زیاد یا dynamic partitioning معمولاً بهترند. routing می‌تواند با client، routing tier یا service discovery انجام شود؛ باید در برابر تغییر membership و failure آگاه باشد.

### قاعدهٔ عملی

&rlm;partition key را از روی queryهای واقعی و نرخ تغییر data انتخاب کنید، نه فقط از روی شناسهٔ ظاهراً مناسب. قبل از production برای hot spot، skew، query چندpartitionی و rebalancing آزمایش انجام دهید. cross-partition transaction و join را استثنا و پرهزینه فرض کنید.

## فصل ۷: <span dir="ltr">Transactions and Concurrency</span>

### ایدهٔ مرکزی

&rlm;`Transaction` چند read و write را به یک unit منطقی تبدیل می‌کند تا application مجبور نباشد همهٔ interleavingهای خراب را خودش مدیریت کند. `ACID` چهار guarantee است، نه یک روش پیاده‌سازی واحد:

- &rlm;`Atomicity`: همهٔ تغییرها commit شوند یا هیچ‌کدام قابل‌مشاهده نباشند.
- &rlm;`Consistency`: invariantهای application بعد از transaction برقرار بمانند؛ این بخش اغلب به منطق application وابسته است.
- &rlm;`Isolation`: transactionهای هم‌زمان نتیجه‌ای مانند اجرای مجاز و جدا از هم بدهند.
- &rlm;`Durability`: بعد از commit، داده در برابر crash از بین نرود.

### نکات کلیدی

&rlm;anomalyهای مهم شامل `dirty read`، `dirty write`، `read skew`، `lost update`، `write skew` و `phantom` هستند. `Read committed` dirty read/write را محدود می‌کند. `Snapshot isolation` با `MVCC` هر transaction را روی snapshot مشخص اجرا می‌کند و read skew را کاهش می‌دهد، اما write skew را الزاماً حل نمی‌کند.

برای `serializability` سه رویکرد اصلی وجود دارد: اجرای واقعاً serial، `Two-Phase Locking (2PL)` با lock و احتمال deadlock، و `Serializable Snapshot Isolation (SSI)` که خوش‌بینانه است و conflict را detect می‌کند. انتخاب isolation باید بر اساس invariant و anomaly قابل‌قبول باشد، نه فقط benchmark.

&rlm;retry بعد از deadlock یا timeout فقط وقتی امن است که operationها با `idempotency key` یا constraint مناسب دوباره اجرا شوند. transaction داخلی یک database با workflow چند service یکی نیست؛ برای workflow توزیع‌شده باید هزینهٔ coordination، `outbox` و `saga` را جداگانه طراحی کرد.

### قاعدهٔ عملی

ابتدا invariantها و anomalyهای خطرناک را بنویسید، سپس کمترین isolation levelی را انتخاب کنید که آن‌ها را واقعاً حفظ کند. transaction را کوتاه نگه دارید، boundary آن را روشن کنید و هر external side effect را طوری طراحی کنید که retry و recovery آن قابل‌اعتماد باشد.

## فصل ۸: <span dir="ltr">Distributed Systems: Failure and Timeouts</span>

### ایدهٔ مرکزی

در distributed system، `partial failure` حالت عادی است: یک node یا network ممکن است خراب یا کند باشد، درحالی‌که بقیه سالم به نظر می‌رسند. نبود response ثابت نمی‌کند request اجرا نشده است؛ ممکن است اجرا شده و reply گم شده باشد. این ابهام ریشهٔ بسیاری از duplicate، data loss و تصمیم‌های اشتباه است.

### نکات کلیدی

شبکه می‌تواند packet را drop، delay، reorder یا duplicate کند. `Timeout` فقط یک حدس عملی دربارهٔ failure است و نباید به‌تنهایی مبنای مالکیت یا تصمیم برگشت‌ناپذیر باشد. retry با backoff و jitter مفید است، اما retry storm می‌تواند خرابی را تشدید کند؛ برای عملیات تکراری از `idempotency` استفاده کنید.

&rlm;clockها نیز قابل‌اعتماد مطلق نیستند: time-of-day ممکن است عقب و جلو شود و clock nodeها با هم یکسان نیستند. برای اندازه‌گیری مدت از `monotonic clock` استفاده کنید و برای ترتیب منطقی eventها از logical clock. process ممکن است به‌علت GC، VM suspend یا scheduler ناگهان pause شود و بعد برگردد، درحالی‌که دیگران آن را مرده دانسته‌اند.

مدل‌های نظری باید صریح باشند: synchronous، partially synchronous یا asynchronous؛ crash-stop یا crash-recovery؛ و در صورت رفتار دروغ‌گو، Byzantine. `Lease`، `quorum` و `fencing token` برای جلوگیری از write کردن actor قدیمی کمک می‌کنند، اما فقط اگر storage token را validate کند. `Safety` یعنی اتفاق بد رخ ندهد و `liveness` یعنی کار سرانجام پیش برود؛ بسیاری از طراحی‌ها یکی را با دیگری معامله می‌کنند.

### قاعدهٔ عملی

فرض‌های failure را مکتوب کنید، timeout و retry را با load test بسنجید، metricهای partial failure را ثبت کنید و مسیر recovery را تمرین کنید. اگر یک machine مسئله را حل می‌کند، distributed complexity را بی‌دلیل اضافه نکنید.

## فصل ۹: <span dir="ltr">Consistency and Consensus</span>

### ایدهٔ مرکزی

&rlm;`Consistency` دربارهٔ آن است که چند client از داده و ترتیب operationها چه می‌بینند؛ `Consensus` دربارهٔ آن است که چند node روی یک تصمیم مشترک و نهایی توافق کنند. این دو مرتبط‌اند، اما یکی نیستند و با `transaction isolation` هم یکی نیستند.

### نکات کلیدی

&rlm;`Eventual consistency` می‌گوید replicaها اگر write متوقف شود سرانجام همگرا می‌شوند، اما زمان یا مقدار intermediate را تضمین نمی‌کند. `Linearizability` طوری رفتار می‌کند که انگار یک copy واحد وجود دارد و هر read بعد از commit، مقدار جدید را می‌بیند. `Serializability` ترتیب transactionها را کنترل می‌کند؛ ممکن است database serializable ولی distributed read آن linearizable نباشد.

&rlm;`Causality` رابطهٔ علت و معلول را حفظ می‌کند، اما الزاماً یک ترتیب کلی نمی‌سازد. `Lamport timestamp` و `happens-before` برای ساختن order سازگار مفیدند. `Total order broadcast` همهٔ nodeها را وادار می‌کند messageها را با ترتیب یکسان deliver کنند و پایهٔ بعضی replicated logهاست.

در `consensus` nodeها باید روی یک value معتبر، غیرقابل‌برگشت و در نهایت مشترک توافق کنند. leader election، lock، uniqueness constraint، membership و atomic commit به آن نزدیک می‌شوند. `Two-Phase Commit (2PC)` atomic commit می‌دهد، اما coordinator می‌تواند failure و blocking ایجاد کند؛ consensus مسئلهٔ گسترده‌تری با guaranteeهای متفاوت است. سرویس‌هایی مانند ZooKeeper و etcd این coordination را آماده ارائه می‌کنند.

### قاعدهٔ عملی

برای هر feature دقیقاً بگویید چه guarantee لازم است. اگر linearizability ضروری نیست، causal یا eventual consistency می‌تواند availability و latency بهتری بدهد. اگر تصمیم مشترک لازم است، از implementation آزموده‌شده استفاده کنید و safety، liveness، failure detection و recovery را جداگانه بسنجید.

## فصل ۱۰: <span dir="ltr">Batch Processing</span>

### ایدهٔ مرکزی

&rlm;`Batch processing` یک input محدود را می‌خواند، transform می‌کند و output مشتق‌شده می‌سازد. چون input معمولاً immutable و قابل‌خواندن دوباره است، batch برای backfill، گزارش، ساخت index و بازسازی view مناسب است. معیار اصلی آن throughput کل job است، نه latency یک request انسانی.

### نکات کلیدی

در الگوی Unix، برنامه‌های کوچک از طریق file و pipe ترکیب می‌شوند. `MapReduce` همین ایده را در مقیاس distributed پیاده می‌کند: mapper داده را می‌خواند، بر اساس key partition می‌کند، مرحلهٔ `shuffle` رکوردهای هم‌key را کنار هم می‌آورد و reducer آن‌ها را aggregate می‌کند. partitioning، sort و انتقال data هزینهٔ اصلی‌اند.

سه الگوی رایج join عبارت‌اند از `sort-merge join` برای inputهای بزرگ، `broadcast hash join` وقتی یکی از inputها کوچک است، و `partitioned hash join` وقتی هر دو input با key یکسان partition شده‌اند. dataflow engineهای جدید می‌توانند intermediate data را کمتر روی disk بنویسند، اما در failure باید بخشی از محاسبه را دوباره انجام دهند.

&rlm;retry کردن task فقط وقتی امن است که operatorها deterministic و بدون side effect خارجی باشند. output را مرحله‌ای و اتمیک publish کنید تا consumer نتیجهٔ ناقص نبیند. batch می‌تواند database مشتق‌شده، recommendation، search index یا aggregate بسازد؛ metadata مربوط به input، version و زمان تولید را نیز نگه دارید.

### قاعدهٔ عملی

&rlm;input را immutable و job را قابل‌بازسازی کنید. pipeline را به stageهای مستقل تقسیم کنید، partition و data skew را اندازه بگیرید و side effect را از محاسبه جدا کنید. batch را فقط برای «کار شبانه» نبینید؛ آن ابزار اصلی اصلاح و بازسازی dataflow است.

## فصل ۱۱: <span dir="ltr">Stream Processing</span>

### ایدهٔ مرکزی

&rlm;`Stream` دنباله‌ای از eventهای پیوسته و معمولاً unbounded است. برخلاف batch، منتظر پایان input نمی‌مانیم؛ هر event یا گروه کوچکی از eventها به‌محض رسیدن پردازش می‌شوند. بنابراین latency کم می‌شود، اما زمان، ترتیب، duplicate و event دیررس باید صریح مدیریت شوند.

### نکات کلیدی

&rlm;`Message broker` می‌تواند پیام را به یک consumer تحویل دهد و پس از acknowledgment حذف کند، یا مانند log-based broker پیام را در partition نگه دارد. در مدل log، consumer با `offset` پیشرفت خود را مشخص می‌کند و می‌تواند با replay state را بازسازی کند. ترتیب معمولاً فقط داخل هر partition تضمین می‌شود؛ key مناسب برای حفظ ترتیب یک entity مهم است.

&rlm;database می‌تواند منبع stream باشد: `Change Data Capture (CDC)` تغییرهای row یا document را منتشر می‌کند و `Event Sourcing` eventهای domain را source of truth می‌گیرد و state را از replay می‌سازد. stream برای materialized view، analytics، `Complex Event Processing` و اتصال چند stream استفاده می‌شود.

باید `event time` را از processing time جدا کرد. `Window` می‌تواند tumbling، hopping، sliding یا session باشد؛ `watermark` اعلام می‌کند تا چه زمانی انتظار event دیررس را داریم. stream-stream join به state و سیاست نگه‌داری نیاز دارد. checkpoint، replay، atomic commit و `Idempotency` برای تحمل failure ضروری‌اند؛ `exactly-once semantics` یک guarantee سرتاسری است، نه چیزی که فقط با نام broker به‌دست آید. `Backpressure` نیز باید جلوی پرشدن حافظه و فروپاشی زنجیره را بگیرد.

### قاعدهٔ عملی

برای هر event schema، key، ordering، duplicate policy، retention و recovery strategy تعیین کنید. پردازش را طوری بنویسید که retry و replay نتیجهٔ یکسان بدهد. اگر freshness خیلی مهم نیست، batch ساده‌تر و قابل‌بازسازی‌تر است؛ stream را برای نیاز واقعی به latency و واکنش پیوسته انتخاب کنید.

## فصل ۱۲: <span dir="ltr">Future of Data Systems</span>

### ایدهٔ مرکزی

هیچ tool واحدی برای storage، search، cache، analytics، recommendation و serving بهترین نیست. معماری آینده بیشتر شبیه یک `dataflow` از source of truth به چند representation تخصصی است. این representationها `derived data` هستند و باید قابل‌ساختن دوباره، قابل‌مشاهده و قابل‌اعتبارسنجی باشند.

### نکات کلیدی

&rlm;`Batch` و `stream` مکمل‌اند: stream تغییرها را با latency کم پخش می‌کند و batch می‌تواند history را دوباره بخواند، خطا را اصلاح کند و view را backfill کند. `Unbundling databases` یعنی قابلیت‌هایی مانند storage، index، replication، query و processing را به componentهای مستقل‌تر تقسیم کنیم؛ سود آن انعطاف است و هزینه‌اش ownership، schema، monitoring، repair و هماهنگی بیشتر.

برای جلوگیری از dual write، `outbox` یعنی تغییر business data و event مربوط به آن در یک transaction محلی ثبت شود و یک relay بعداً event را منتشر کند. `Idempotency` یعنی اجرای دوبارهٔ یک operation اثر جدیدی ایجاد نکند؛ برای retry، replay و duplicate event ضروری است. `Saga` زنجیره‌ای از transactionهای محلی است که در صورت شکست با `compensating action` جبران می‌شود؛ saga atomicity سراسری ایجاد نمی‌کند، پس stateهای میانی و جبران ناقص باید پذیرفته و قابل‌مشاهده باشند.

درستی باید end-to-end بررسی شود. `Timeliness` یعنی داده به‌موقع باشد؛ `Integrity` یعنی خراب یا دست‌کاری نشده باشد؛ `Auditability` یعنی بتوان فهمید چه کسی، چه زمانی و بر اساس کدام input و version نتیجه را ساخته است. بعضی constraintها مانند uniqueness به coordination قوی نیاز دارند، اما بعضی invariantها با validation بعدی و compensating action بهتر scale می‌شوند.

داده دربارهٔ انسان‌هاست. predictive analytics می‌تواند bias و feedback loop بسازد؛ tracking می‌تواند به surveillance تبدیل شود. privacy، امکان اعتراض، حداقل‌سازی داده، retention، حذف از cache و model و مسئولیت تصمیم باید از ابتدا بخشی از design باشند، نه وصلهٔ انتهایی.

### قاعدهٔ عملی

برای هر derived view پنج سؤال بپرسید: source of truth چیست؟ چگونه ساخته می‌شود؟ چگونه freshness و correctness آن سنجیده می‌شود؟ در صورت خرابی چگونه replay یا rebuild می‌شود؟ و با دادهٔ کاربر چگونه منصفانه و قابل‌اعتراض رفتار می‌کند؟
