# طراحی سامانه‌های داده‌محور

## Designing Data-Intensive Applications

این branch یک **ترجمهٔ کامل برای مطالعهٔ شخصی** از کتاب مارتین کلپمن است. اصطلاحات فنی مانند `document`، `relational`، `normalization`، `denormalization` و `rebalancing` به شکل اصلی باقی می‌مانند و با توضیح ساده همراه می‌شوند.

## فهرست مطالب

### پیشگفتار

- [پیشگفتار](./preface/README.md)

### Part I: Foundations of Data Systems

| فصل | عنوان                                                                                               | وضعیت           |
| --- | --------------------------------------------------------------------------------------------------- | --------------- |
| ۱   | [Reliability, Scalability, Maintainability](./chapters/01-reliable-scalable-maintainable/README.md) | ترجمه شده |
| ۲   | [Data Models و Query Languages](./chapters/02-data-models-query-languages/README.md)                | ترجمه شده |
| ۳   | [Storage و Retrieval](./chapters/03-storage-retrieval/README.md)                                    | ترجمه شده |
| ۴   | [Encoding و Evolution](./chapters/04-encoding-evolution/README.md)                                  | ترجمه شده |

### Part II: Distributed Data

| فصل | عنوان                                                                                 | وضعیت           |
| --- | ------------------------------------------------------------------------------------- | --------------- |
| ۵   | [Replication](./chapters/05-replication/README.md)                                    | ترجمه شده |
| ۶   | [Partitioning و Sharding](./chapters/06-partitioning/README.md)                       | ترجمه شده |
| ۷   | [Transactions و Concurrency](./chapters/07-transactions/README.md)                    | ترجمه شده |
| ۸   | [Distributed Systems: Failure و Timeout](./chapters/08-distributed-systems/README.md) | ترجمه شده |
| ۹   | [Consistency و Consensus](./chapters/09-consistency-consensus/README.md)              | ترجمه شده |

### Part III: Derived Data

| فصل | عنوان                                                                    | وضعیت           |
| --- | ------------------------------------------------------------------------ | --------------- |
| ۱۰  | [Batch Processing](./chapters/10-batch-processing/README.md)             | ترجمه شده |
| ۱۱  | [Stream Processing](./chapters/11-stream-processing/README.md)           | ترجمه شده |
| ۱۲  | [Future of Data Systems](./chapters/12-future-of-data-systems/README.md) | ترجمه شده |

### منابع داخلی پروژه

- [واژه‌نامهٔ اصطلاحات](./glossary/README.md)
- [راهنمای یکدستی اصطلاحات](./TERMINOLOGY.md)
- [راهنمای سبک نگارش](./STYLE_GUIDE.md)
- [راهنمای مشارکت](./CONTRIBUTING.md)

## روش مطالعه

پیشنهاد می‌شود ابتدا پیشگفتار و فصل اول خوانده شود و سپس فصل‌ها به‌ترتیب پیش بروند. فصل‌های ۵ تا ۹ بر مفاهیم سامانه‌های توزیع‌شده تمرکز دارند و فصل‌های ۱۰ تا ۱۲ نشان می‌دهند چگونه از دادهٔ خام، دادهٔ مشتق‌شده و جریان‌های پردازشی ساخته می‌شود. اگر از صفر شروع می‌کنید، ابتدا [راهنمای سبک نگارش](./STYLE_GUIDE.md) و واژه‌نامه را بخوانید.

در هر فصل، اصطلاح انگلیسی در اولین کاربرد آمده است. نام technologyها، APIها، protocolها و codeها ترجمه نشده‌اند تا تطبیق آن‌ها با مستندات فنی آسان بماند.

figureهای فصل‌ها از PDF استخراج شده‌اند و متن توضیحی آن‌ها به فارسی برگردانده شده است.

## مشارکت

برای اصلاح خطاهای مفهومی یا زبانی، ابتدا [راهنمای مشارکت](./CONTRIBUTING.md) را بخوانید. Pull Requestها باید فصل، بخش تغییرکرده و دلیل اصلاح را روشن کنند.
