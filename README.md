# طراحی سامانه‌های داده‌محور

## Designing Data-Intensive Applications

این مخزن ترجمهٔ فارسی کتاب **Designing Data-Intensive Applications** نوشتهٔ **Martin Kleppmann** است. کتاب دربارهٔ طراحی سامانه‌های داده‌محورِ reliable، scalable و maintainable است و موضوعاتی مانند data model، storage، replication، distributed systems، transaction، batch processing و stream processing را بررسی می‌کند.

فصل‌ها با نثر فارسی روان و آموزشی ترجمه شده‌اند. برای حفظ دقت فنی، نام اصطلاحات تخصصی، ابزارها، APIها و روش‌ها در کنار توضیح فارسی آن‌ها به شکل اصلی آورده شده‌اند و مثال‌ها و figureهای مرتبط نیز در هر فصل قرار گرفته‌اند.

<h2 dir="rtl" align="right">فهرست مطالب</h2>

<h3 dir="rtl" align="right">پیشگفتار</h3>

<ul dir="rtl" align="right">
  <li><a href="./preface/README.md">پیشگفتار</a></li>
</ul>

<h3 dir="rtl" align="right">بخش اول: <span dir="ltr">Foundations of Data Systems</span></h3>

<ul dir="rtl" align="right">
  <li><a href="./chapters/01-reliable-scalable-maintainable/README.md">فصل ۱: <span dir="ltr">Reliability, Scalability, Maintainability</span></a></li>
  <li><a href="./chapters/02-data-models-query-languages/README.md">فصل ۲: <span dir="ltr">Data Models</span> و <span dir="ltr">Query Languages</span></a></li>
  <li><a href="./chapters/03-storage-retrieval/README.md">فصل ۳: <span dir="ltr">Storage</span> و <span dir="ltr">Retrieval</span></a></li>
  <li><a href="./chapters/04-encoding-evolution/README.md">فصل ۴: <span dir="ltr">Encoding</span> و <span dir="ltr">Evolution</span></a></li>
</ul>

<h3 dir="rtl" align="right">بخش دوم: <span dir="ltr">Distributed Data</span></h3>

<ul dir="rtl" align="right">
  <li><a href="./chapters/05-replication/README.md">فصل ۵: <span dir="ltr">Replication</span></a></li>
  <li><a href="./chapters/06-partitioning/README.md">فصل ۶: <span dir="ltr">Partitioning</span> و <span dir="ltr">Sharding</span></a></li>
  <li><a href="./chapters/07-transactions/README.md">فصل ۷: <span dir="ltr">Transactions</span> و <span dir="ltr">Concurrency</span></a></li>
  <li><a href="./chapters/08-distributed-systems/README.md">فصل ۸: <span dir="ltr">Distributed Systems: Failure</span> و <span dir="ltr">Timeout</span></a></li>
  <li><a href="./chapters/09-consistency-consensus/README.md">فصل ۹: <span dir="ltr">Consistency</span> و <span dir="ltr">Consensus</span></a></li>
</ul>

<h3 dir="rtl" align="right">بخش سوم: <span dir="ltr">Derived Data</span></h3>

<ul dir="rtl" align="right">
  <li><a href="./chapters/10-batch-processing/README.md">فصل ۱۰: <span dir="ltr">Batch Processing</span></a></li>
  <li><a href="./chapters/11-stream-processing/README.md">فصل ۱۱: <span dir="ltr">Stream Processing</span></a></li>
  <li><a href="./chapters/12-future-of-data-systems/README.md">فصل ۱۲: <span dir="ltr">Future of Data Systems</span></a></li>
</ul>

<h3 dir="rtl" align="right">منابع داخلی پروژه</h3>

<ul dir="rtl" align="right">
  <li><a href="./glossary/README.md">واژه‌نامهٔ اصطلاحات</a></li>
  <li><a href="./TERMINOLOGY.md">راهنمای یکدستی اصطلاحات</a></li>
  <li><a href="./STYLE_GUIDE.md">راهنمای سبک نگارش</a></li>
  <li><a href="./CONTRIBUTING.md">راهنمای مشارکت</a></li>
</ul>

## روش مطالعه

پیشنهاد می‌شود ابتدا پیشگفتار و فصل اول خوانده شود و سپس فصل‌ها به‌ترتیب پیش بروند. فصل‌های ۵ تا ۹ بر مفاهیم سامانه‌های توزیع‌شده تمرکز دارند و فصل‌های ۱۰ تا ۱۲ نشان می‌دهند چگونه از دادهٔ خام، دادهٔ مشتق‌شده و جریان‌های پردازشی ساخته می‌شود. اگر از صفر شروع می‌کنید، ابتدا [راهنمای سبک نگارش](./STYLE_GUIDE.md) و واژه‌نامه را بخوانید.

در هر فصل، اصطلاح انگلیسی در اولین کاربرد آمده است. نام technologyها، APIها، protocolها و codeها ترجمه نشده‌اند تا تطبیق آن‌ها با مستندات فنی آسان بماند.

figureهای فصل‌ها از PDF استخراج شده‌اند و متن توضیحی آن‌ها به فارسی برگردانده شده است.

## مشارکت

برای اصلاح خطاهای مفهومی یا زبانی، ابتدا [راهنمای مشارکت](./CONTRIBUTING.md) را بخوانید. Pull Requestها باید فصل، بخش تغییرکرده و دلیل اصلاح را روشن کنند.
