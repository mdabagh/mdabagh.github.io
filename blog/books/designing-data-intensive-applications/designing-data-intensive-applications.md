> **راهنمای مطالعه**
>
> این صفحه معرفی کلی کتاب است. یادداشت‌های هر فصل در صفحه‌ی همان فصل آمده؛ در هر بخش ابتدا جمله‌ی کلیدی متن اصلی به انگلیسی و سپس ترجمه و توضیح فارسی آن ارائه شده است.

---
---
title: "طراحی برنامه‌های داده‌محور"
author: "مارتین کلپمن (Martin Kleppmann)"
original_title: "Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems"
publisher: "O'Reilly Media"
year: "2017"
translator: "ترجمه به فارسی"
tags: [distributed-systems, databases, replication, partitioning, transactions, stream-processing]
---

# طراحی برنامه‌های داده‌محور

**نویسنده:** مارتین کلپمن (Martin Kleppmann)  
**ناشر:** O'Reilly Media  
**سال انتشار:** ۲۰۱۷  
**ویرایش اول**

---

## این کتاب درباره‌ی چیست؟

بیشتر برنامه‌های امروزی **داده‌محور** (Data-Intensive) هستند، نه محاسبه‌محور: مشکل اصلی آن‌ها قدرت پردازنده نیست، بلکه حجم داده، پیچیدگی داده و سرعت تغییر آن است. این کتاب به‌جای آموزش یک ابزار خاص، اصول و بده‌بستان‌های پشت پایگاه‌های داده، صف‌های پیام، کش‌ها، موتورهای جستجو و سیستم‌های پردازش دسته‌ای و جریانی را توضیح می‌دهد تا بتوانید برای هر مسئله ابزار درست را انتخاب کنید و آن‌ها را درست کنار هم بگذارید.

سه هدف اصلی که در تمام کتاب تکرار می‌شوند:

- **قابلیت اطمینان** (Reliability): سیستم حتی در حضور خطای سخت‌افزار، نرم‌افزار و انسان درست کار کند.
- **مقیاس‌پذیری** (Scalability): با رشد حجم داده، ترافیک یا پیچیدگی، راه معقولی برای کنار آمدن با بار وجود داشته باشد.
- **نگهداشت‌پذیری** (Maintainability): افراد مختلف در طول زمان بتوانند سیستم را به‌راحتی اداره کنند، بفهمند و تغییر دهند.

---

## ساختار کتاب

### بخش اول: مبانی سیستم‌های داده (Foundations of Data Systems)

- [پیش‌گفتار: درباره‌ی این کتاب](post.html?cat=books&slug=designing-data-intensive-applications/0-about-this-book)
- [فصل ۱: برنامه‌های قابل‌اعتماد، مقیاس‌پذیر و نگهداشت‌پذیر](post.html?cat=books&slug=designing-data-intensive-applications/1-reliable-scalable-maintainable)
- [فصل ۲: مدل‌های داده و زبان‌های پرس‌وجو](post.html?cat=books&slug=designing-data-intensive-applications/2-data-models-query-languages)
- [فصل ۳: ذخیره‌سازی و بازیابی](post.html?cat=books&slug=designing-data-intensive-applications/3-storage-retrieval)
- [فصل ۴: کدگذاری و تکامل](post.html?cat=books&slug=designing-data-intensive-applications/4-encoding-evolution)

### بخش دوم: داده‌ی توزیع‌شده (Distributed Data)

- [فصل ۵: تکثیر](post.html?cat=books&slug=designing-data-intensive-applications/5-replication)
- [فصل ۶: پارتیشن‌بندی](post.html?cat=books&slug=designing-data-intensive-applications/6-partitioning)
- [فصل ۷: تراکنش‌ها](post.html?cat=books&slug=designing-data-intensive-applications/7-transactions)
- [فصل ۸: دردسرهای سیستم‌های توزیع‌شده](post.html?cat=books&slug=designing-data-intensive-applications/8-trouble-distributed-systems)
- [فصل ۹: سازگاری و اجماع](post.html?cat=books&slug=designing-data-intensive-applications/9-consistency-consensus)

### بخش سوم: داده‌ی مشتق‌شده (Derived Data)

- [فصل ۱۰: پردازش دسته‌ای](post.html?cat=books&slug=designing-data-intensive-applications/10-batch-processing)
- [فصل ۱۱: پردازش جریانی](post.html?cat=books&slug=designing-data-intensive-applications/11-stream-processing)

> **نکته:** نسخه‌ی PDF موجود، نسخه‌ی Early Release کتاب است و فصل ۱۲ (The Future of Data Systems) را ندارد؛ به همین دلیل یادداشت‌ها تا فصل ۱۱ پیش رفته‌اند.

---

## پیوند با سایر نوشته‌های وبلاگ

- [System Design Interview](book.html?cat=books&slug=design-system) — نسخه‌ی مصاحبه‌محور بسیاری از همین مفاهیم.
- [Dynamo: Amazon's Highly Available Key-value Store](post.html?cat=article&slug=dynamo-paper) — نمونه‌ی واقعی تکثیر بدون رهبر و پارتیشن‌بندی با هشینگ سازگار (فصل ۵ و ۶).
- [Cassandra](post.html?cat=article&slug=cassandra-paper) و [Scaling Memcache at Facebook](post.html?cat=article&slug=scaling-memcache-at-facebook) — کاربرد عملی تکثیر و کش در مقیاس بزرگ.
- [Galera Replication](post.html?cat=article&slug=galera-replication) — تکثیر هم‌زمان در دیتابیس‌های رابطه‌ای (فصل ۵ و ۷).
