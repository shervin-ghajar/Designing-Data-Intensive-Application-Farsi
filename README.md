# طراحی سامانه‌های داده‌محور

## Designing Data-Intensive Applications

این مخزن یک **راهنمای آموزشی مستقل و زمینه‌محور** دربارهٔ ایده‌های کتاب مارتین کلپمن است. هر فصل علاوه بر خلاصه، توضیح گام‌به‌گام، جدول تصمیم، سناریوی طراحی، نمودارهای مستقل Mermaid و تمرین‌های مرور دارد؛ این مخزن ترجمهٔ خط‌به‌خط یا نسخهٔ فارسی رسمی کتاب نیست.

> **وضعیت حقوق نشر:** کتاب اصلی © ۲۰۱۷ Martin Kleppmann و O'Reilly Media است. برای انتشار عمومی ترجمهٔ کامل، مجوز صاحب حق نشر لازم است. ذکر نام نویسنده جایگزین مجوز انتشار نیست. این پروژه PDF کتاب، تصاویر اصلی یا متن‌های طولانیِ عیناً کپی‌شده را توزیع نمی‌کند.

## فهرست مطالب

### پیشگفتار

- [پیشگفتار](./preface/README.md)

### Part I: Foundations of Data Systems

| فصل | عنوان | وضعیت |
| --- | --- | --- |
| ۱ | [Reliability, Scalability, Maintainability](./chapters/01-reliable-scalable-maintainable/README.md) | راهنمای کامل‌تر |
| ۲ | [Data Models و Query Languages](./chapters/02-data-models-query-languages/README.md) | راهنمای کامل‌تر |
| ۳ | [Storage و Retrieval](./chapters/03-storage-retrieval/README.md) | راهنمای کامل‌تر |
| ۴ | [Encoding و Evolution](./chapters/04-encoding-evolution/README.md) | راهنمای کامل‌تر |

### Part II: Distributed Data

| فصل | عنوان | وضعیت |
| --- | --- | --- |
| ۵ | [Replication](./chapters/05-replication/README.md) | راهنمای کامل‌تر |
| ۶ | [Partitioning و Sharding](./chapters/06-partitioning/README.md) | راهنمای کامل‌تر |
| ۷ | [Transactions و Concurrency](./chapters/07-transactions/README.md) | راهنمای کامل‌تر |
| ۸ | [Distributed Systems: Failure و Timeout](./chapters/08-distributed-systems/README.md) | راهنمای کامل‌تر |
| ۹ | [Consistency و Consensus](./chapters/09-consistency-consensus/README.md) | راهنمای کامل‌تر |

### Part III: Derived Data

| فصل | عنوان | وضعیت |
| --- | --- | --- |
| ۱۰ | [Batch Processing](./chapters/10-batch-processing/README.md) | راهنمای کامل‌تر |
| ۱۱ | [Stream Processing](./chapters/11-stream-processing/README.md) | راهنمای کامل‌تر |
| ۱۲ | [Future of Data Systems](./chapters/12-future-of-data-systems/README.md) | راهنمای کامل‌تر |

### منابع داخلی پروژه

- [واژه‌نامهٔ اصطلاحات](./glossary/README.md)
- [راهنمای یکدستی اصطلاحات](./TERMINOLOGY.md)
- [راهنمای سبک نگارش](./STYLE_GUIDE.md)
- [راهنمای مشارکت](./CONTRIBUTING.md)
- [مرزهای حقوقی و دامنهٔ استفاده](./RIGHTS.md)

## روش مطالعه

پیشنهاد می‌شود ابتدا پیشگفتار و فصل اول خوانده شود و سپس فصل‌ها به‌ترتیب پیش بروند. فصل‌های ۵ تا ۹ بر مفاهیم سامانه‌های توزیع‌شده تمرکز دارند و فصل‌های ۱۰ تا ۱۲ نشان می‌دهند چگونه از دادهٔ خام، دادهٔ مشتق‌شده و جریان‌های پردازشی ساخته می‌شود. اگر از صفر شروع می‌کنید، ابتدا [راهنمای سبک نگارش](./STYLE_GUIDE.md) و واژه‌نامه را بخوانید.

در هر فصل، اصطلاح انگلیسی در اولین کاربرد آمده است. نام فناوری‌ها، APIها، پروتکل‌ها و قطعه‌کدها ترجمه نشده‌اند تا تطبیق آن‌ها با مستندات فنی آسان بماند.

نمودارهای Mermaid، مثال‌ها، جدول‌ها و تمرین‌های این مخزن برای همین راهنما از نو طراحی شده‌اند و شکل‌های کتاب نیستند.

## مشارکت

برای اصلاح خطاهای مفهومی یا زبانی، ابتدا [راهنمای مشارکت](./CONTRIBUTING.md) را بخوانید. Pull Requestها باید خلاصه‌ای مستقل ارائه دهند و نباید متن طولانی کتاب، شکل‌های اصلی یا PDF آن را بازنشر کنند.
