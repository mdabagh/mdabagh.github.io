# ترجمه فارسی: Cassandra - A Decentralized Structured Storage System

> **مقاله اصلی:** Cassandra - A Decentralized Structured Storage System
> **نویسندگان:** Avinash Lakshman, Prashant Malik (Facebook)
> **منبع:** LADIS 2009
> **فایل PDF:** cassandra-paper.pdf

---

## چکیده

> Cassandra is a distributed storage system for managing very large amounts of structured data spread out across many commodity servers, while providing highly available service with no single point of failure.

Cassandra یک سیستم ذخیره‌سازی توزیع‌شده برای مدیریت مقادیر بسیار زیادی داده ساختاریافته است که در سرورهای ارزان قیمت پراکنده شده و سرویس با دسترسی بالا و بدون نقطه خرابی واحد ارائه می‌دهد.

---

## مقدمه

> Facebook runs the largest social networking platform that serves hundreds of millions users at peak times using tens of thousands of servers located in many data centers around the world.

Facebook بزرگترین پلتفرم شبکه اجتماعی را اجرا می‌کند که در زمان‌های پیک صدها میلیون کاربر را با ده‌ها هزار سرور در مراکز داده مختلف جهان سرویس می‌دهد.

---

## مدل داده

> A table in Cassandra is a distributed multi dimensional map indexed by a key. The value is an object which is highly structured.

جدول در Cassandra یک نقشه چندبعدی توزیع‌شده است که با کلید ایندکس می‌شود. مقدار یک شیء بسیار ساختاریافته است.

> Columns are grouped together into sets called column families very much similar to what happens in the Bigtable system.

ستون‌ها در مجموعه‌هایی به نام خانواده‌های ستون گروه‌بندی می‌شوند، بسیار مشابه آنچه در سیستم Bigtable اتفاق می‌افتد.

---

## معماری سیستم

### پارتیشن‌بندی

> Cassandra partitions data across the cluster using consistent hashing but uses an order preserving hash function to do so.

Cassandra داده‌ها را در خوشه با هشینگ سازگار پارتیشن‌بندی می‌کند اما از تابع هش حفظ‌کننده ترتیب استفاده می‌کند.

> In consistent hashing the output range of a hash function is treated as a fixed circular space or "ring". Each node in the system is assigned a random value within this space which represents its position on the ring.

در هشینگ سازگار، محدوده خروجی تابع هش به عنوان یک فضای دایره‌ای ثابت یا "حلقه" در نظر گرفته می‌شود. هر گره در سیستم مقدار تصادفی در این فضا اختصاص داده می‌شود که موقعیت آن را روی حلقه نشان می‌دهد.

### ریپلیکیشن

> Cassandra uses replication to achieve high availability and durability. Each data item is replicated at N hosts, where N is the replication factor.

Cassandra از ریپلیکیشن برای دستیابی به دسترسی بالا و دوام استفاده می‌کند. هر قلم داده در N میزبان ریپلیک می‌شود که N عامل ریپلیکیشن است.

---

## الگوریتم‌های توزیع‌شده

### تشخیص خرابی

> Cassandra uses a gossip based membership protocol to maintain the liveness information for each member in the cluster.

Cassandra از پروتکل عضویت مبتنی بر Gossip برای حفظ اطلاعات زنده بودن هر عضو در خوشه استفاده می‌کند.

### هماهنگی نوشتن

> Cassandra uses a quorum-based protocol for writes. The coordinator contacts all replicas for a given key and waits for a quorum of acknowledgements.

Cassandra از پروتکل مبتنی برorum برای نوشتن استفاده می‌کند. هماهنگ‌کننده با تمام ریپلیکاها برای کلید داده شده تماس می‌گیرد و منتظر تأییدorum می‌ماند.

---

## یادداشت شخصی

> **اهمیت این مقاله:** Cassandra یکی از مهمترین سیستم‌های NoSQL است که توسط Facebook برای جستجوی Inbox توسعه یافت. استفاده از هشینگ سازگار برای پارتیشن‌بندی و مدل جدول ساده آن الهام‌بخش بسیاری از سیستم‌های بعدی بوده است.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Cassandra Paper](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf)
