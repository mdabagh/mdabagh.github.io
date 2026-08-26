> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۷۱

> **CHAPTER 5: DESIGN CONSISTENT HASHING**
> To achieve horizontal scaling, it is important to distribute requests/data efficiently and evenly across servers. Consistent hashing is a commonly used technique to achieve this goal. But first, let us take an in-depth look at the problem.

**فصل ۵: طراحی هشینگ یکپارچه (Consistent Hashing)**

برای دستیابی به **مقیاس‌پذیری افقی (Horizontal Scaling)**، توزیع کارآمد و یکنواخت درخواست‌ها/داده‌ها بین سرورها اهمیت زیادی دارد. **هشینگ یکپارچه (Consistent Hashing)** تکنیکی رایج برای دستیابی به این هدف است. اما ابتدا بیایید مشکل را عمیق‌تر بررسی کنیم.

---

###### 📄 صفحه ۷۲

> **The rehashing problem**
> If you have n cache servers, a common way to balance the load is to use the following hash method:
> serverIndex = hash(key) % N, where N is the size of the server pool.
>
> Let us use an example to illustrate how it works. As shown in Table 5-1, we have 4 servers and 8 string keys with their hashes.
>
> To fetch the server where a key is stored, we perform the modular operation f(key) % 4. For instance, hash(key0) % 4 = 1 means a client must contact server 1 to fetch the cached data.
> Figure 5-1 shows the distribution of keys based on Table 5-1.

### مشکل هش مجدد (Rehashing Problem)

اگر **n** سرور کش داشته باشید، روش رایجی برای بالانس کردن بار استفاده از روش هش زیر است:

```
serverIndex = hash(key) % N
```

که در آن **N** اندازه مجموعه سرورها است.

بیایید با یک مثال نحوه عملکرد آن را توضیح دهیم. همان‌طور که در جدول ۵-۱ نشان داده شده، ۴ سرور و ۸ کلید رشته‌ای با هش‌هایشان داریم.

برای یافتن سروری که یک کلید در آن ذخیره شده، عملیات باقی‌مانده `f(key) % 4` را انجام می‌دهیم. برای مثال، `hash(key0) % 4 = 1` به این معناست که کلاینت باید با **سرور ۱** تماس بگیرد تا داده کش‌شده را دریافت کند.

شکل ۵-۱ توزیع کلیدها بر اساس جدول ۵-۱ را نشان می‌دهد.

![Figure 5-1](design-system/images/System-Design-Interview-page72-image1.jpg)

---

###### 📄 صفحه ۷۳

> This approach works well when the size of the server pool is fixed, and the data distribution is even. However, problems arise when new servers are added, or existing servers are removed. For example, if server 1 goes offline, the size of the server pool becomes 3. Using the same hash function, we get the same hash value for a key. But applying modular operation gives us different server indexes because the number of servers is reduced by 1. We get the results as shown in Table 5-2 by applying hash % 3:
>
> Figure 5-2 shows the new distribution of keys based on Table 5-2.

این رویکرد زمانی خوب عمل می‌کند که **اندازه مجموعه سرورها ثابت** باشد و توزیع داده یکنواخت باشد. اما مشکلات زمانی پیش می‌آید که سرورهای جدیدی اضافه یا سرورهای موجود حذف شوند.

برای مثال، اگر **سرور ۱** آفلاین شود، اندازه مجموعه سرورها به ۳ تغییر می‌کند. با استفاده از همان تابع هش، مقدار هش یکسانی برای یک کلید دریافت می‌کنیم. اما اعمال عملیات باقی‌مانده شاخص‌های سرور متفاوتی به ما می‌دهد زیرا تعداد سرورها ۱ واحد کاهش یافته است. نتایج زیر با اعمال `hash % 3` به دست می‌آیند (جدول ۵-۲):

شکل ۵-۲ توزیع جدید کلیدها بر اساس جدول ۵-۲ را نشان می‌دهد.

![Figure 5-2](design-system/images/System-Design-Interview-page73-image1.jpg)

---

###### 📄 صفحه ۷۴

> As shown in Figure 5-2, most keys are redistributed, not just the ones originally stored in the offline server (server 1). This means that when server 1 goes offline, most cache clients will connect to the wrong servers to fetch data. This causes a storm of cache misses. Consistent hashing is an effective technique to mitigate this problem.

همان‌طور که در شکل ۵-۲ نشان داده شده، **بیشتر کلیدها دوباره توزیع می‌شوند**، نه فقط کلیدهایی که در ابتدا در سرور آفلاین (سرور ۱) ذخیره شده بودند. این به این معناست که وقتی سرور ۱ آفلاین می‌شود، بیشتر کلاینت‌های کش به **سرورهای اشتباه** متصل می‌شوند تا داده‌ها را دریافت کنند. این اتفاق **طوفان کش میس (Cache Miss Storm)** را ایجاد می‌کند.

**هشینگ یکپارچه (Consistent Hashing)** تکنیکی مؤثر برای کاهش این مشکل است.

![Figure 5-3](design-system/images/System-Design-Interview-page73-image2.jpg)

---

###### 📄 صفحه ۷۵

> **Consistent hashing**
> Quoted from Wikipedia: "Consistent hashing is a special kind of hashing such that when a hash table is re-sized and consistent hashing is used, only k/n keys need to be remapped on average, where k is the number of keys, and n is the number of slots. In contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped [1].
>
> **Hash space and hash ring**
> Now we understand the definition of consistent hashing, let us find out how it works. Assume SHA-1 is used as the hash function f, and the output range of the hash function is: x0, x1, x2, x3, ..., xn. In cryptography, SHA-1's hash space goes from 0 to 2^160 - 1. That means x0 corresponds to 0, xn corresponds to 2^160 - 1, and all the other hash values in the middle fall between 0 and 2^160 - 1. Figure 5-3 shows the hash space.
>
> By collecting both ends, we get a hash ring as shown in Figure 5-4:

### هشینگ یکپارچه (Consistent Hashing)

به نقل از ویکی‌پدیا: «هشینگ یکپارچه نوع خاصی از هشینگ است که در آن وقتی اندازه یک جدول هش تغییر می‌کند و از هشینگ یکپارچه استفاده می‌شود، به‌طور متوسط فقط **k/n** کلید نیاز به بازتوانی (Remap) دارند، که در آن **k** تعداد کلیدها و **n** تعداد شکاف‌ها (Slots) است. در مقابل، در بیشتر جداول هش سنتی، تغییر تعداد شکاف‌های آرایه باعث بازتوانی تقریباً تمام کلیدها می‌شود [۱].»

### فضای هش و حلقه هش

حالا که تعریف هشینگ یکپارچه را درک کردیم، بیایید نحوه عملکرد آن را بررسی کنیم. فرض کنید **SHA-1** به‌عنوان تابع هش **f** استفاده شود و بازه خروجی تابع هش شامل مقادیر **x0, x1, x2, x3, ..., xn** باشد. در رمزنگاری، فضای هش SHA-1 از ۰ تا **2^160 - 1** است. یعنی x0 معادل ۰، xn معادل 2^160 - 1 و تمام مقادیر هش دیگر بین ۰ و 2^160 - 1 قرار دارند. شکل ۵-۳ فضای هش را نشان می‌دهد.

با اتصال دو انتهای فضای هش، یک **حلقه هش (Hash Ring)** به دست می‌آوریم (شکل ۵-۴):

![Figure 5-4](design-system/images/System-Design-Interview-page75-image1.jpg)

---

###### 📄 صفحه ۷۵ (ادامه)

> **Hash servers:** Using the same hash function f, we map servers based on server IP or name onto the ring. Figure 5-5 shows that 4 servers are mapped on the hash ring.

### سرورهای هش

با استفاده از همان تابع هش **f**، سرورها را بر اساس IP یا نام سرور روی حلقه نگاشت می‌کنیم. شکل ۵-۵ نشان می‌دهد ۴ سرور روی حلقه هش نگاشت شده‌اند.

![Figure 5-5](design-system/images/System-Design-Interview-page75-image2.jpg)

---

###### 📄 صفحه ۷۶

> **Hash keys:** One thing worth mentioning is that hash function used here is different from the one in "the rehashing problem," and there is no modular operation. As shown in Figure 5-6, 4 cache keys (key0, key1, key2, and key3) are hashed onto the hash ring.

### کلیدهای هش

نکته قابل ذکر این است که تابع هش مورد استفاده در اینجا با تابع هش در «مشکل هش مجدد» متفاوت است و **عملیات باقی‌مانده (Modular Operation) وجود ندارد**. همان‌طور که در شکل ۵-۶ نشان داده شده، ۴ کلید کش (key0, key1, key2, key3) روی حلقه هش هش شده‌اند.

![Figure 5-6](design-system/images/System-Design-Interview-page76-image1.jpg)

![Figure 5-7](design-system/images/System-Design-Interview-page76-image2.jpg)

---

###### 📄 صفحه ۷۷

> **Server lookup:** To determine which server a key is stored on, we go clockwise from the key position on the ring until a server is found. Figure 5-7 explains this process. Going clockwise, key0 is stored on server 0; key1 is stored on server 1; key2 is stored on server 2 and key3 is stored on server 3.
>
> **Add a server:** Using the logic described above, adding a new server will only require redistribution of a fraction of keys. In Figure 5-8, after a new server 4 is added, only key0 needs to be redistributed. k1, k2, and k3 remain on the same servers.

### جستجوی سرور (Server Lookup)

برای تعیین اینکه یک کلید روی کدام سرور ذخیره شده، **از موقعیت کلید روی حلقه در جهت عقربه ساعت حرکت می‌کنیم** تا اولین سرور پیدا شود. شکل ۵-۷ این فرایند را توضیح می‌دهد. در جهت عقربه ساعت:
- **key0** روی **سرور ۰** ذخیره شده
- **key1** روی **سرور ۱** ذخیره شده
- **key2** روی **سرور ۲** ذخیره شده
- **key3** روی **سرور ۳** ذخیره شده

### اضافه کردن سرور

با استفاده از منطق بالا، اضافه کردن سرور جدید فقط نیاز به **بازتوزیع کسری از کلیدها** دارد. در شکل ۵-۸، پس از اضافه شدن سرور ۴، فقط **key0** نیاز به بازتوزیع دارد. k1, k2, k3 در همان سرورهای قبلی باقی می‌مانند.

![Figure 5-8](design-system/images/System-Design-Interview-page77-image1.jpg)

---

###### 📄 صفحه ۷۸

> **Remove a server:** When a server is removed, only a small fraction of keys require redistribution with consistent hashing. In Figure 5-9, when server 1 is removed, only key1 must be remapped to server 2. The rest of the keys are unaffected.

### حذف سرور

وقتی سروری حذف می‌شود، فقط **کسر کوچکی از کلیدها** نیاز به بازتوزیع با هشینگ یکپارچه دارند. در شکل ۵-۹، وقتی سرور ۱ حذف می‌شود، فقط **key1** باید به سرور ۲ بازتوانی شود. بقیه کلیدها تحت تأثیر قرار نمی‌گیرند.

![Figure 5-9](design-system/images/System-Design-Interview-page78-image1.jpg)

---

###### 📄 صفحه ۷۹

> **Two issues in the basic approach:** The consistent hashing algorithm was introduced by Karger et al. at MIT [1]. The basic steps are:
> • Map servers and keys on to the ring using a uniformly distributed hash function.
> • To find out which server a key is mapped to, go clockwise from the key position until the first server on the ring is found.
>
> Two problems are identified with this approach. First, it is impossible to keep the same size of partitions on the ring for all servers considering a server can be added or removed. A partition is the hash space between adjacent servers. It is possible that the size of the partitions on the ring assigned to each server is very small or fairly large. In Figure 5-10, if s1 is removed, s2's partition (highlighted with the bidirectional arrows) is twice as large as s0 and s3's partition.

### دو مشکل در رویکرد پایه

الگوریتم هشینگ یکپارچه توسط **Karger و همکاران در MIT** معرفی شد [۱]. مراحل پایه:

- نگاشت سرورها و کلیدها روی حلقه با استفاده از تابع هش **یکنواخت توزیع‌شده**.
- برای یافتن سروری که کلید به آن نگاشت شده، از موقعیت کلید در جهت عقربه ساعت حرکت کنید تا اولین سرور روی حلقه پیدا شود.

**دو مشکل** در این رویکرد شناسایی شده است:

**مشکل اول:** با توجه به اینکه سرور ممکن است اضافه یا حذف شود، غیرممکن است اندازه **پارتیشن‌ها** روی حلقه برای تمام سرورها یکسان باشد. پارتیشن فضای هش بین سرورهای مجاور است. ممکن است اندازه پارتیشن‌های اختصاص‌یافته به هر سرور بسیار کوچک یا نسبتاً بزرگ باشد. در شکل ۵-۱۰، اگر s1 حذف شود، پارتیشن s2 (بزرگ‌تر شده) **دو برابر** پارتیشن s0 و s3 است.

![Figure 5-10](design-system/images/System-Design-Interview-page79-image1.jpg)

---

###### 📄 صفحه ۸۰

> Second, it is possible to have a non-uniform key distribution on the ring. For instance, if servers are mapped to positions listed in Figure 5-11, most of the keys are stored on server 2. However, server 1 and server 3 have no data.
>
> A technique called virtual nodes or replicas is used to solve these problems.
>
> **Virtual nodes:** A virtual node refers to the real node, and each server is represented by multiple virtual nodes on the ring. In Figure 5-12, both server 0 and server 1 have 3 virtual nodes. The 3 is arbitrarily chosen; and in real-world systems, the number of virtual nodes is much larger. Instead of using s0, we have s0_0, s0_1, and s0_2 to represent server 0 on the ring. Similarly, s1_0, s1_1, and s1_2 represent server 1 on the ring. With virtual nodes, each server is responsible for multiple partitions. Partitions (edges) with label s0 are managed by server 0. On the other hand, partitions with label s1 are managed by server 1.

**مشکل دوم:** ممکن است **توزیع ناهمگون کلیدها** روی حلقه وجود داشته باشد. برای مثال، اگر سرورها به موقعیت‌های فهرست‌شده در شکل ۵-۱۱ نگاشت شوند، بیشتر کلیدها روی **سرور ۲** ذخیره می‌شوند، در حالی که سرور ۱ و سرور ۳ هیچ داده‌ای ندارند.

تکنیکی به نام **گره‌های مجازی (Virtual Nodes)** یا **نسخه‌ها (Replicas)** برای حل این مشکلات استفاده می‌شود.

### گره‌های مجازی (Virtual Nodes)

گره مجازی به گره واقعی اشاره دارد و هر سرور توسط **چندین گره مجازی** روی حلقه نمایش داده می‌شود. در شکل ۵-۱۲، هر دو سرور ۰ و سرور ۱ دارای ۳ گره مجازی هستند. عدد ۳ به‌صورت دلخواه انتخاب شده و در سیستم‌های واقعی تعداد گره‌های مجازی بسیار بیشتر است.

به جای استفاده از s0، از **s0_0, s0_1, s0_2** برای نمایش سرور ۰ روی حلقه استفاده می‌شود. به همین ترتیب، **s1_0, s1_1, s1_2** سرور ۱ را نمایش می‌دهند. با گره‌های مجازی، هر سرور مسئول **چندین پارتیشن** است. پارتیشن‌های برچسب‌دار s0 توسط سرور ۰ مدیریت می‌شوند و پارتیشن‌های برچسب‌دار s1 توسط سرور ۱.

![Figure 5-11](design-system/images/System-Design-Interview-page80-image1.jpg)

![Figure 5-12](design-system/images/System-Design-Interview-page80-image2.jpg)

---

###### 📄 صفحه ۸۱

> To find which server a key is stored on, we go clockwise from the key's location and find the first virtual node encountered on the ring. In Figure 5-13, to find out which server k0 is stored on, we go clockwise from k0's location and find virtual node s1_1, which refers to server 1.

برای یافتن سروری که کلید روی آن ذخیره شده، از موقعیت کلید در جهت عقربه ساعت حرکت می‌کنیم و **اولین گره مجازی** که روی حلقه با آن مواجه می‌شویم را پیدا می‌کنیم.

در شکل ۵-۱۳، برای یافتن سرور k0، از موقعیت k0 در جهت عقربه ساعت حرکت کرده و گره مجازی **s1_1** را پیدا می‌کنیم که به **سرور ۱** اشاره دارد.

![Figure 5-13](design-system/images/System-Design-Interview-page81-image1.jpg)

---

###### 📄 صفحه ۸۲

> As the number of virtual nodes increases, the distribution of keys becomes more balanced. This is because the standard deviation gets smaller with more virtual nodes, leading to balanced data distribution. Standard deviation measures how data are spread out. The outcome of an experiment carried out by online research [2] shows that with one or two hundred virtual nodes, the standard deviation is between 5% (200 virtual nodes) and 10% (100 virtual nodes) of the mean.
>
> However, more spaces are needed to store data about virtual nodes. This is a tradeoff, and we can tune the number of virtual nodes to fit our system requirements.
>
> **Find affected keys:** When a server is added or removed, a fraction of data needs to be redistributed. How can we find the affected range to redistribute the keys?
>
> In Figure 5-14, server 4 is added onto the ring. The affected range starts from s4 (newly added node) and moves anticlockwise around the ring until a server is found (s3). Thus, keys located between s3 and s4 need to be redistributed to s4.

با افزایش تعداد گره‌های مجازی، **توزیع کلیدها متعادل‌تر** می‌شود. این به این دلیل است که با گره‌های مجازی بیشتر، **انحراف معیار کاهش** می‌یابد که به توزیع متعادل داده منجر می‌شود. نتایج یک آزمایش آنلاین [۲] نشان می‌دهد که با ۱۰۰ تا ۲۰۰ گره مجازی، انحراف معیار بین ۵٪ (۲۰۰ گره مجازی) و ۱۰٪ (۱۰۰ گره مجازی) میانگین است.

بااین‌حال، فضای بیشتری برای ذخیره اطلاعات گره‌های مجازی نیاز است. این یک **مبادله (Tradeoff)** است و می‌توانیم تعداد گره‌های مجازی را برای تطابق با نیازمندی‌های سیستم تنظیم کنیم.

### یافتن کلیدهای تحت تأثیر

وقتی سروری اضافه یا حذف می‌شود، کسری از داده‌ها نیاز به بازتوزیع دارد. چگونه محدوده تحت تأثیر را برای بازتوزیع کلیدها پیدا کنیم؟

در شکل ۵-۱۴، سرور ۴ به حلقه اضافه شده است. **محدوده تحت تأثیر از s4 (گره جدید) شروع شده و در جهت عکس عقربه ساعت** دور حلقه حرکت می‌کند تا سروری پیدا شود (s3). بنابراین، کلیدهای موجود بین s3 و s4 باید به s4 بازتوزیع شوند.

![Figure 5-14](design-system/images/System-Design-Interview-page82-image1.jpg)

---

###### 📄 صفحه ۸۳

> When a server (s1) is removed as shown in Figure 5-15, the affected range starts from s1 (removed node) and moves anticlockwise around the ring until a server is found (s0). Thus, keys located between s0 and s1 must be redistributed to s2.

وقتی سرور (s1) همان‌طور که در شکل ۵-۱۵ نشان داده شده حذف می‌شود، محدوده تحت تأثیر از **s1 (گره حذف‌شده) شروع شده و در جهت عکس عقربه ساعت** دور حلقه حرکت می‌کند تا سروری پیدا شود (s0). بنابراین، کلیدهای موجود بین s0 و s1 باید به **s2** بازتوزیع شوند.

![Figure 5-15](design-system/images/System-Design-Interview-page83-image1.jpg)

![Figure 5-16](design-system/images/System-Design-Interview-page83-image2.jpg)

---

###### 📄 صفحه ۸۵

> **Wrap up:** In this chapter, we had an in-depth discussion about consistent hashing, including why it is needed and how it works. The benefits of consistent hashing include:
> • Minimized keys are redistributed when servers are added or removed.
> • It is easy to scale horizontally because data are more evenly distributed.
> • Mitigate hotspot key problem. Excessive access to a specific shard could cause server overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. Consistent hashing helps to mitigate the problem by distributing the data more evenly.
>
> Consistent hashing is widely used in real-world systems, including some notable ones:
> • Partitioning component of Amazon's Dynamo database [3]
> • Data partitioning across the cluster in Apache Cassandra [4]
> • Discord chat application [5]
> • Akamai content delivery network [6]
> • Maglev network load balancer [7]
>
> Congratulations on getting this far! Now give yourself a pat on the back. Good job!

### جمع‌بندی

در این فصل، بحث عمیقی درباره هشینگ یکپارچه داشتیم، از جمله اینکه چرا به آن نیاز است و چگونه کار می‌کند. **مزایای هشینگ یکپارچه** شامل موارد زیر است:

- **حداقل بازتوزیع کلیدها** هنگام اضافه یا حذف سرورها.
- **مقیاس‌پذیری افقی آسان** زیرا داده‌ها یکنواخت‌تر توزیع می‌شوند.
- **کاهش مشکل کلید داغ (Hotspot Key Problem):** دسترسی بیش از حد به یک شارد خاص می‌تواند باعث بیش‌باری سرور شود. فرض کنید داده‌های **Katy Perry**، **Justin Bieber** و **Lady Gaga** همه در یک شارد قرار بگیرند. هشینگ یکپارچه با توزیع یکنواختتر داده‌ها به کاهش این مشکل کمک می‌کند.

هشینگ یکپارچه به‌طور گسترده‌ای در سیستم‌های واقعی استفاده می‌شود، از جمله:

- مؤلفه پارتیشن‌بندی **پایگاه داده Dynamo آمازون [۳]**
- پارتیشن‌بندی داده در خوشه **Apache Cassandra [۴]**
- اپلیکیشن چت **Discord [۵]**
- شبکه توزیع محتوای **Akamai [۶]**
- بالانسر بار شبکه **Maglev [۷]**

تبریک! تا اینجا پیش رفتید. حالا به خودتان یک آفرین بگویید. آفرین!

---

### مواد مرجع

[۱] Consistent hashing: https://en.wikipedia.org/wiki/Consistent_hashing
> ***یادداشت شخصی***
> 🔗 [ویکی‌پدیا: هشینگ سازگار](https://en.wikipedia.org/wiki/Consistent_hashing) - مرجع اولیه تعریف هشینگ سازگار

[۲] Consistent Hashing: https://tom-e-white.com/2007/11/consistent-hashing.html
> ***یادداشت شخصی***
> 🔗 [ترجمه کامل مقاله Tom White](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=ConsistentHashingTomWhite) - بهترین توضیح ساده و عملی از هشینگ سازگار با پیاده‌سازی Java

[۳] Dynamo: Amazon's Highly Available Key-value Store: https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf
> ***یادداشت شخصی***
> 🔗 [ترجمه کامل مقاله Dynamo](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=DynamoPaper) - مقاله اصلی آمازون که هشینگ سازگار را برای پارتیشن‌بندی داده معرفی کرد

[۴] Cassandra - A Decentralized Structured Storage System: http://www.cs.cornell.edu/Projects/ladis2009/papers/Lakshman-ladis2009.PDF
> ***یادداشت شخصی***
> 🔗 [ترجمه کامل مقاله Cassandra](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=CassandraPaper) - سیستم NoSQL فیسبوک که از هشینگ سازگار برای پارتیشن‌بندی استفاده می‌کند

[۵] How Discord Scaled Elixir to 5,000,000 Concurrent Users: https://blog.discord.com/scaling-elixir-f9b8e1e7c29b
> ***یادداشت شخصی***
> 🔗 [ترجمه کامل مقاله Discord](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=DiscordScaling) - چگونه Discord تریلیون‌ها پیام را با هشینگ سازگار ایندکس می‌کند

[۶] CS168: The Modern Algorithmic Toolbox Lecture #1: Introduction and Consistent Hashing: http://theory.stanford.edu/~tim/s16/l/l1.pdf
> ***یادداشت شخصی***
> 🔗 [یادداشت‌های CS168 Stanford](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=CS168ConsistentHashing) - پایه‌های الگوریتمی هشینگ سازگار از دوره استنفورد

[۷] Maglev: A Fast and Reliable Software Network Load Balancer: https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/44824.pdf
> ***یادداشت شخصی***
> 🔗 [ترجمه کامل مقاله Maglev](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=MaglevPaper) - متعادل‌کننده بار شبکه گوگل که از هشینگ سازگار استفاده می‌کند
