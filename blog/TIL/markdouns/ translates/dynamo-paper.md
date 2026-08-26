# ترجمه فارسی مقاله Dynamo: فایل ذخیره‌سازی کلید-مقدار بسیار در دسترس آمازون

> **مقاله اصلی:** Dynamo: Amazon's Highly Available Key-value Store
> **نویسندگان:** Giuseppe DeCandia, Deniz Hastorun, Madan Jampani, Gunavardhan Kakulapati, Avinash Lakshman, Alex Pilchin, Swaminathan Sivasubramanian, Peter Vosshall and Werner Vogels
> **منبع:** Amazon.com - SOSP'07, October 14-17, 2007, Stevenson, Washington, USA

---

## چکیده

> Reliability at massive scale is one of the biggest challenges we face at Amazon.com, one of the largest e-commerce operations in the world; even the slightest outage has significant financial consequences and impacts customer trust.

قابلیت اطمینان در مقیاس بزرگ یکی از بزرگ‌ترین چالش‌هایی است که با آن در آمازون - یکی از بزرگ‌ترین عملیات‌های تجارت الکترونیک در جهان - روبرو هستیم. کوچک‌ترین قطعی نیز پیامدهای مالی قابل توجهی دارد و بر اعتماد مشتریان تأثیر می‌گذارد.

> The Amazon.com platform, which provides services for many web sites worldwide, is implemented on top of an infrastructure of tens of thousands of servers and network components located in many datacenters around the world. At this scale, small and large components fail continuously and the way persistent state is managed in the face of these failures drives the reliability and scalability of the software systems.

پلتفرم آمازون که خدماتی را برای وب‌سایت‌های متعدد در سراسر جهان ارائه می‌دهد، بر روی زیرساختی شامل ده‌ها هزار سرور و مؤلفه شبکه‌ای که در مراکز داده متعدد در سراسر جهان قرار دارند، پیاده‌سازی شده است. در این مقیاس، مؤلفه‌های کوچک و بزرگ به طور مداوم خراب می‌شوند و نحوه مدیریت وضعیت پایدار در مواجهه با این خرابی‌ها، قابلیت اطمینان و مقیاس‌پذیری سیستم‌های نرم‌افزاری را تعیین می‌کند.

> This paper presents the design and implementation of Dynamo, a highly available key-value storage system that some of Amazon's core services use to provide an "always-on" experience. To achieve this level of availability, Dynamo sacrifices consistency under certain failure scenarios. It makes extensive use of object versioning and application-assisted conflict resolution in a manner that provides a novel interface for developers to use.

این مقاله طراحی و پیاده‌سازی Dynamo را ارائه می‌دهد، یک سیستم ذخیره‌سازی کلید-مقدار بسیار در دسترس که برخی از خدمات اصلی آمازون برای ارائه تجربه "همیشه روشن" از آن استفاده می‌کنند. برای دستیابی به این سطح از در دسترس بودن، Dynamo در سناریوهای خرابی خاص، سازگاری را قربانی می‌کند. این سیستم به طور گسترده از نسخه‌بندی اشیا و حل تعارض با کمک برنامه‌های کاربردی استفاده می‌کند به نحوی که رابط نوینی را برای توسعه‌دهندگان فراهم می‌کند.

---

## ۱. مقدمه

> Amazon runs a world-wide e-commerce platform that serves tens of millions customers at peak times using tens of thousands of servers located in many data centers around the world. There are strict operational requirements on Amazon's platform in terms of performance, reliability and efficiency, and to support continuous growth the platform needs to be highly scalable. Reliability is one of the most important requirements because even the slightest outage has significant financial consequences and impacts customer trust.

آمازون یک پلتفرم تجارت الکترونیک جهانی را اجرا می‌کند که در زمان‌های اوج، ده‌ها میلیون مشتری را با استفاده از ده‌ها هزار سرور واقع در مراکز داده متعدد در سراسر جهان پوشش می‌دهد. الزامات عملیاتی سختگیرانه‌ای از نظر عملکرد، قابلیت اطمینان و کارایی بر پلتفرم آمازون حاکم است و برای پشتیبانی از رشد مداوم، پلتفرم باید بسیار مقیاس‌پذیر باشد. قابلیت اطمینان یکی از مهم‌ترین الزامات است زیرا حتی کوچک‌ترین قطعی نیز پیامدهای مالی قابل توجهی دارد و بر اعتماد مشتریان تأثیر می‌گذارد.

> One of the lessons our organization has learned from operating Amazon's platform is that the reliability and scalability of a system is dependent on how its application state is managed. Amazon uses a highly decentralized, loosely coupled, service oriented architecture consisting of hundreds of services. In this environment there is a particular need for storage technologies that are always available. For example, customers should be able to view and add items to their shopping cart even if disks are failing, network routes are flapping, or data centers are being destroyed by tornados.

یکی از درس‌هایی که سازمان ما از اداره پلتفرم آمازون آموخته این است که قابلیت اطمینان و مقیاس‌پذیری یک سیستم به نحوه مدیریت وضعیت برنامه کاربردی آن بستگی دارد. آمازون از معماری بسیار غیرمتمرکز، شل و مبتنی بر سرویس شامل صدها سرویس استفاده می‌کند. در این محیط، نیاز ویژه‌ای به فناوری‌های ذخیره‌سازی وجود دارد که همیشه در دسترس باشند. به عنوان مثال، مشتریان باید بتوانند کالاها را مشاهده و به سبد خرید خود اضافه کنند، حتی اگر دیسک‌ها خراب شوند، مسیرهای شبکه ناپایدار باشند یا مراکز داده توسط طوفان نابود شوند.

> To meet the reliability and scaling needs, Amazon has developed a number of storage technologies, of which the Amazon Simple Storage Service (also available outside of Amazon and known as Amazon S3), is probably the best known. This paper presents the design and implementation of Dynamo, another highly available and scalable distributed data store built for Amazon's platform.

برای برآورده کردن نیازهای قابلیت اطمینان و مقیاس‌پذیری، آمازون تعدادی فناوری ذخیره‌سازی توسعه داده است که از جمله آنها Amazon Simple Storage Service (که خارج از آمازون نیز موجود است و به نام Amazon S3 شناخته می‌شود) احتمالاً شناخته‌شده‌ترین است. این مقاله طراحی و پیاده‌سازی Dynamo را ارائه می‌دهد که یک فروشگاه داده توزیع شده بسیار در دسترس و مقیاس‌پذیر دیگر است که برای پلتفرم آمازون ساخته شده است.

> Dynamo uses a synthesis of well known techniques to achieve scalability and availability: Data is partitioned and replicated using consistent hashing, and consistency is facilitated by object versioning. The consistency among replicas during updates is maintained by a quorum-like technique and a decentralized replica synchronization protocol.

Dynamo از ترکیبی از تکنیک‌های شناخته شده برای دستیابی به مقیاس‌پذیری و در دسترس بودن استفاده می‌کند: داده‌ها با استفاده از هشینگ سازگار پارتیشن‌بندی و تکرار می‌شوند و سازگاری از طریق نسخه‌بندی اشیا تسهیل می‌شود. سازگاری بین نسخه‌ها در حین به‌روزرسانی‌ها توسط تکنیکی مشابه کворوم و پروتکل همگام‌سازی نسخه غیرمتمرکز حفظ می‌شود.

> Dynamo employs a gossip based distributed failure detection and membership protocol. Dynamo is a completely decentralized system with minimal need for manual administration. Storage nodes can be added and removed from Dynamo without requiring any manual partitioning or redistribution.

Dynamo از پروتکل تشخیص خرابی توزیع شده و عضویت مبتنی بر Gossip استفاده می‌کند. Dynamo یک سیستم کاملاً غیرمتمرکز با حداقل نیاز به مدیریت دستی است. گره‌های ذخیره‌سازی می‌توانند بدون نیاز به پارتیشن‌بندی یا توزیع مجدد دستی به Dynamo اضافه یا از آن حذف شوند.

> In the past year, Dynamo has been the underlying storage technology for a number of the core services in Amazon's e-commerce platform. It was able to scale to extreme peak loads efficiently without any downtime during the busy holiday shopping season. For example, the service that maintains shopping cart (Shopping Cart Service) served tens of millions requests that resulted in well over 3 million checkouts in a single day and the service that manages session state handled hundreds of thousands of concurrently active sessions.

در سال گذشته، Dynamo فناوری ذخیره‌سازی زیربنایی برای تعدادی از خدمات اصلی در پلتفرم تجارت الکترونیک آمازون بوده است. این سیستم توانست به طور کارآمد به بارهای اوج شدید مقیاس یابد و بدون هیچ زمان توقفی در فصل خرید شلوغ تعطیلات کار کند. به عنوان مثال، سرویسی که سبد خرید را مدیریت می‌کند (Shopping Cart Service) ده‌ها میلیون درخواست را پردازش کرد که منجر به بیش از ۳ میلیون پرداخت در یک روز شد و سرویسی که وضعیت نشست را مدیریت می‌کند صدها هزار نشست فعال همزمان را مدیریت کرد.

---

## ۲. پیش‌زمینه

> Amazon's e-commerce platform is composed of hundreds of services that work in concert to deliver functionality ranging from recommendations to order fulfillment to fraud detection. Each service is exposed through a well defined interface and is accessible over the network. These services are hosted in an infrastructure that consists of tens of thousands of servers located across many data centers world-wide. Some of these services are stateless (i.e., services which aggregate responses from other services) and some are stateful (i.e., a service that generates its response by executing business logic on its state stored in persistent store).

پلتفرم تجارت الکترونیک آمازون از صدها سرویس تشکیل شده است که به طور هماهنگ کار می‌کنند تا عملکردهایی از توصیه‌های شخصی‌سازی شده تا اجرای سفارشات و تشخیص تقلب ارائه دهند. هر سرویس از طریق یک رابط تعریف شده خوب در معرض نمایش قرار می‌گیرد و از طریق شبکه قابل دسترسی است. این سرویس‌ها در زیرساختی میزبانی می‌شوند که از ده‌ها هزار سرور در مراکز داده متعدد در سراسر جهان تشکیل شده است. برخی از این سرویس‌ها بی‌狀態 (یعنی سرویس‌هایی که پاسخ‌های سرویس‌های دیگر را جمع‌آوری می‌کنند) و برخی دیگر دارای حالت (یعنی سرویسی که پاسخ خود را با اجرای منطق تجاری بر روی حالت ذخیره شده در فروشگاه پایدار تولید می‌کند) هستند.

> Traditionally production systems store their state in relational databases. For many of the more common usage patterns of state persistence, however, a relational database is a solution that is far from ideal. Most of these services only store and retrieve data by primary key and do not require the complex querying and management functionality offered by an RDBMS.

به طور سنتی، سیستم‌های تولیدی حالت خود را در پایگاه‌های داده رابطه‌ای ذخیره می‌کنند. با این حال، برای بسیاری از الگوهای رایج‌تر استفاده از پایداری حالت، پایگاه داده رابطه‌ای راه‌حلی بسیار دور از ایده‌آل است. بیشتر این سرویس‌ها فقط داده‌ها را بر اساس کلید اولیه ذخیره و بازیابی می‌کنند و به عملکردهای پیچیده پرس‌وجو و مدیریت ارائه شده توسط RDBMS نیاز ندارند.

> This paper describes Dynamo, a highly available data storage technology that addresses the needs of these important classes of services. Dynamo has a simple key/value interface, is highly available with a clearly defined consistency window, is efficient in its resource usage, and has a simple scale out scheme to address growth in data set size or request rates.

این مقاله Dynamo را توصیف می‌کند، یک فناوری ذخیره‌سازی داده بسیار در دسترس که نیازهای این طبقات مهم از سرویس‌ها را برآورده می‌کند. Dynamo یک رابط ساده کلید/مقدار دارد، بسیار در دسترس با پنجره سازگاری به وضوح تعریف شده است، در استفاده از منابع کارآمد است و یک طرح مقیاس‌بندی ساده برای مقابله با رشد اندازه مجموعه داده یا نرخ درخواست‌ها دارد.

### ۲.۱ الزامات و فرضیات سیستم

> **Query Model:** simple read and write operations to a data item that is uniquely identified by a key. State is stored as binary objects (i.e., blobs) identified by unique keys. No operations span multiple data items and there is no need for relational schema. Dynamo targets applications that need to store objects that are relatively small (usually less than 1 MB).

**مدل پرس‌وجو:** عملیات خواندن و نوشتن ساده بر روی یک قلم داده که توسط یک کلید به طور منحصربفرد شناسایی می‌شود. حالت به صورت اشیای دودویی (یعنی blobs) ذخیره می‌شود که توسط کلیدهای منحصربفرد شناسایی می‌شوند. هیچ عملیاتی شامل چندین قلم داده نمی‌شود و نیازی به اسکیمای رابطه‌ای نیست. Dynamo برای برنامه‌های کاربردی طراحی شده است که نیاز به ذخیره اشیای نسبتاً کوچک (معمولاً کمتر از ۱ مگابایت) دارند.

> **ACID Properties:** Dynamo targets applications that operate with weaker consistency (the "C" in ACID) if this results in high availability. Dynamo does not provide any isolation guarantees and permits only single key updates.

**ویژگی‌های ACID:** Dynamo برای برنامه‌های کاربردی طراحی شده است که با سازگاری ضعیف‌تر (حرف "C" در ACID) عمل می‌کنند اگر این امر منجر به در دسترس بودن بالا شود. Dynamo هیچ تضمین جداسازی ارائه نمی‌دهد و فقط اجازه به‌روزرسانی تک کلید را می‌دهد.

> **Efficiency:** The system needs to function on a commodity hardware infrastructure. In Amazon's platform, services have stringent latency requirements which are in general measured at the 99.9th percentile of the distribution. Services must be able to configure Dynamo such that they consistently achieve their latency and throughput requirements.

**کارایی:** سیستم باید بر روی زیرسخت‌افزار استاندارد عمل کند. در پلتفرم آمازون، سرویس‌ها الزامات سختگیرانه تأخیر دارند که به طور کلی در صدک ۹۹.۹ توزیع اندازه‌گیری می‌شوند. سرویس‌ها باید بتوانند Dynamo را به گونه‌ای پیکربندی کنند که به طور مداوم الزامات تأخیر و توان عملیاتی خود را برآورده کنند.

### ۲.۲ توافقات سطح سرویس (SLA)

> To guarantee that the application can deliver its functionality in a bounded time, each and every dependency in the platform needs to deliver its functionality with even tighter bounds. Clients and services engage in a Service Level Agreement (SLA), a formally negotiated contract where a client and a service agree on several system-related characteristics, which most prominently include the client's expected request rate distribution for a particular API and the expected service latency under those conditions.

برای تضمین اینکه برنامه کاربردی می‌تواند عملکرد خود را در زمان محدود ارائه دهد، هر وابستگی در پلتفرم باید عملکرد خود را با محدودیت‌های حتی سخت‌تر ارائه دهد. مشتریان و سرویس‌ها یک توافقنامه سطح سرویس (SLA) منعقد می‌کنند، قراردادی که به طور رسمی مذاکره شده و در آن مشتری و سرویس بر چندین ویژگی مرتبط با سیستم توافق می‌کنند که مهم‌ترین آنها شامل توزیع نرخ درخواست مورد انتظار مشتری برای یک API خاص و تأخیر سرویس مورد انتظار تحت آن شرایط است.

> An example of a simple SLA is a service guaranteeing that it will provide a response within 300ms for 99.9% of its requests for a peak client load of 500 requests per second.

یک نمونه از یک SLA ساده این است که یک سرویس تضمین کند که پاسخی را ظرف ۳۰۰ میلی‌ثانیه برای ۹۹.۹٪ از درخواست‌های خود در بار اوج مشتری یعنی ۵۰۰ درخواست در ثانیه ارائه خواهد داد.

> In this paper there are many references to this 99.9th percentile of distributions, which reflects Amazon engineers' relentless focus on performance from the perspective of the customers' experience.

در این مقاله ارجاعات زیادی به این صدک ۹۹.۹ توزیع‌ها وجود دارد که تمرکز بی‌وقفه مهندسان آمازون بر عملکرد از دیدگاه تجربه مشتریان را منعکس می‌کند.

### ۲.۳ ملاحظات طراحی

> From the very early replicated database works, it is well known that when dealing with the possibility of network failures, strong consistency and high data availability cannot be achieved simultaneously. As such systems and applications need to be aware which properties can be achieved under which conditions.

از اولین کارهای پایگاه داده تکرار شده، به خوبی مشخص است که وقتی با احتمال خرابی شبکه سر و کار داریم، سازگاری قوی و در دسترس بودن بالای داده نمی‌توانند به طور همزمان محقق شوند. بنابراین سیستم‌ها و برنامه‌های کاربردی باید بدانند که چه ویژگی‌هایی تحت چه شرایطی قابل دستیابی هستند.

> For systems prone to server and network failures, availability can be increased by using optimistic replication techniques, where changes are allowed to propagate to replicas in the background, and concurrent, disconnected work is tolerated. The challenge with this approach is that it can lead to conflicting changes which must be detected and resolved.

برای سیستم‌هایی که در معرض خرابی سرور و شبکه هستند، در دسترس بودن می‌تواند با استفاده از تکنیک‌های تکرار خوش‌بینانه افزایش یابد، جایی که تغییرات اجازه می‌یابند در پس‌زمینه به نسخه‌ها منتشر شوند و کار همزمان و قطع شده تحمل می‌شود. چالش این رویکرد این است که می‌تواند منجر به تغییرات متعارض شود که باید شناسایی و حل شوند.

> Dynamo is designed to be an eventually consistent data store; that is all updates reach all replicas eventually. An important design consideration is to decide when to perform the process of resolving update conflicts, i.e., whether conflicts should be resolved during reads or writes.

Dynamo برای یک فروشگاه داده سازگار نهایی طراحی شده است؛ یعنی تمام به‌روزرسانی‌ها در نهایت به تمام نسخه‌ها می‌رسند. یک ملاحظه طراحی مهم تصمیم‌گیری در مورد زمان انجام فرآیند حل تعارضات به‌روزرسانی است، یعنی اینکه آیا تعارضات باید در حین خواندن‌ها یا نوشتن‌ها حل شوند.

> For a number of Amazon services, rejecting customer updates could result in a poor customer experience. For instance, the shopping cart service must allow customers to add and remove items from their shopping cart even amidst network and server failures. This requirement forces us to push the complexity of conflict resolution to the reads in order to ensures that writes are never rejected.

برای تعدادی از سرویس‌های آمازون، رد کردن به‌روزرسانی‌های مشتری می‌تواند منجر به تجربه ضعیف مشتری شود. به عنوان مثال، سرویس سبد خرید باید به مشتریان اجازه دهد کالاها را به سبد خرید خود اضافه و از آن حذف کنند، حتی در میان خرابی‌های شبکه و سرور. این الزام ما را مجبور می‌کند پیچیدگی حل تعارض را به خواندن‌ها منتقل کنیم تا اطمینان حاصل شود که نوشتن‌ها هرگز رد نمی‌شوند.

> The next design choice is who performs the process of conflict resolution. This can be done by the data store or the application. If conflict resolution is done by the data store, its choices are rather limited. In such cases, the data store can only use simple policies, such as "last write wins", to resolve conflicting updates.

انتخاب طراحی بعدی این است که چه کسی فرآیند حل تعارض را انجام می‌دهد. این کار می‌تواند توسط فروشگاه داده یا برنامه کاربردی انجام شود. اگر حل تعارض توسط فروشگاه داده انجام شود، انتخاب‌های آن نسبتاً محدود هستند. در چنین مواردی، فروشگاه داده فقط می‌تواند از سیاست‌های ساده مانند "آخرین نوشتن برنده است" برای حل به‌روزرسانی‌های متعارض استفاده کند.

> Other key principles embraced in the design are:
> - **Incremental scalability:** Dynamo should be able to scale out one storage host at a time, with minimal impact on both operators of the system and the system itself.
> - **Symmetry:** Every node in Dynamo should have the same set of responsibilities as its peers; there should be no distinguished node or nodes that take special roles or extra set of responsibilities.
> - **Decentralization:** An extension of symmetry, the design should favor decentralized peer-to-peer techniques over centralized control.
> - **Heterogeneity:** The system needs to be able to exploit heterogeneity in the infrastructure it runs on.

اصول کلیدی دیگری که در طراحی رعایت شده‌اند:
- **مقیاس‌پذیری تدریجی:** Dynamo باید بتواند یک میزبان ذخیره‌سازی را در هر زمان با حداقل تأثیر بر هم اپراتورهای سیستم و هم خود سیستم مقیاس‌بندی کند.
- **تقارن:** هر گره در Dynamo باید مجموعه مسئولیت‌های یکسانی با همتایان خود داشته باشد؛ نباید گره یا گره‌های متمایزی وجود داشته باشند که نقش‌های ویژه یا مجموعه مسئولیت‌های اضافی بر عهده بگیرند.
- **غیرمتمرکز بودن:** گستره‌ای از تقارن، طراحی باید تکنیک‌های همتا-به-همتای غیرمتمرکز را بر کنترل متمرکز ترجیح دهد.
- **ناهمگونی:** سیستم باید بتواند از ناهمگونی در زیرساختی که روی آن اجرا می‌شود بهره‌برداری کند.

---

## ۴. معماری سیستم

### ۴.۱ رابط سیستم

> Dynamo stores objects associated with a key through a simple interface; it exposes two operations: get() and put(). The get(key) operation locates the object replicas associated with the key in the storage system and returns a single object or a list of objects with conflicting versions along with a context. The put(key, context, object) operation determines where the replicas of the object should be placed based on the associated key, and writes the replicas to disk.

Dynamo اشیای مرتبط با یک کلید را از طریق یک رابط ساده ذخیره می‌کند؛ دو عملیات را در معرض نمایش قرار می‌دهد: get() و put(). عملیات get(key) نسخه‌های اشیای مرتبط با کلید را در سیستم ذخیره‌سازی مکان‌یابی می‌کند و یک شیء واحد یا لیستی از اشیا با نسخه‌های متعارض همراه با زمینه برمی‌گرداند. عملیات put(key, context, object) تعیین می‌کند که نسخه‌های شیء بر اساس کلید مرتبط کجا باید قرار داده شوند و نسخه‌ها را بر روی دیسک می‌نویسد.

### ۴.۲ الگوریتم پارتیشن‌بندی

> One of the key design requirements for Dynamo is that it must scale incrementally. This requires a mechanism to dynamically partition the data over the set of nodes in the system. Dynamo's partitioning scheme relies on consistent hashing to distribute the load across multiple storage hosts. In consistent hashing, the output range of a hash function is treated as a fixed circular space or "ring" (i.e. the largest hash value wraps around to the smallest hash value).

یکی از الزامات طراحی کلیدی Dynamo این است که باید به طور تدریجی مقیاس‌بندی شود. این نیازمند مکانیزمی برای پارتیشن‌بندی پویای داده‌ها بر روی مجموعه گره‌ها در سیستم است. طرح پارتیشن‌بندی Dynamo بر هشینگ سازگار برای توزیع بار بر چندین میزبان ذخیره‌سازی تکیه دارد. در هشینگ سازگار، بازه خروجی تابع هش به عنوان فضای دایره‌ای ثابت یا "حلقه" در نظر گرفته می‌شود (یعنی بزرگترین مقدار هش به کوچکترین مقدار هش برمی‌گردد).

> The basic consistent hashing algorithm presents some challenges. First, the random position assignment of each node on the ring leads to non-uniform data and load distribution. Second, the basic algorithm is oblivious to the heterogeneity in the performance of nodes. To address these issues, Dynamo uses a variant of consistent hashing: instead of mapping a node to a single point in the circle, each node gets assigned to multiple points in the ring. To this end, Dynamo uses the concept of "virtual nodes".

الگوریتم پایه‌ای هشینگ سازگار چالش‌هایی را ارائه می‌دهد. اول، تخصیص تصادفی موقعیت هر گره روی حلقه منجر به توزیع ناهموار داده و بار می‌شود. دوم، الگوریتم پایه‌ای نسبت به ناهمگونی در عملکرد گره‌ها بی‌توجه است. برای حل این مشکلات، Dynamo از گونه‌ای از هشینگ سازگار استفاده می‌کند: به جای نگاشت یک گره به یک نقطه واحد در دایره، هر گره به چندین نقطه در حلقه تخصیص داده می‌شود. برای این منظور Dynamo از مفهوم "گره‌های مجازی" استفاده می‌کند.

> Using virtual nodes has the following advantages:
> - If a node becomes unavailable (due to failures or routine maintenance), the load handled by this node is evenly dispersed across the remaining available nodes.
> - When a node becomes available again, or a new node is added to the system, the newly available node accepts a roughly equivalent amount of load from each of the other available nodes.
> - The number of virtual nodes that a node is responsible can decided based on its capacity, accounting for heterogeneity in the physical infrastructure.

استفاده از گره‌های مجازی مزایای زیر را دارد:
- اگر یک گره در دسترس نباشد (به دلیل خرابی یا تعمیر و نگهداری معمول)، بار مدیریت شده توسط این گره به طور مساوی در بین گره‌های در دسترس باقیمانده توزیع می‌شود.
- وقتی یک گره دوباره در دسترس می‌شود یا یک گره جدید به سیستم اضافه می‌شود، گره جدید در دسترس مقدار تقریباً معادلی از بار را از هر یک از گره‌های در دسترس دیگر می‌پذیرد.
- تعداد گره‌های مجازی که یک گره مسئول آن است می‌تواند بر اساس ظرفیت آن تعیین شود و ناهمگونی در زیرساخت فیزیکی را در نظر بگیرد.

### ۴.۳ تکرار

> To achieve high availability and durability, Dynamo replicates its data on multiple hosts. Each data item is replicated at N hosts, where N is a parameter configured "per-instance". Each key, k, is assigned to a coordinator node. The coordinator is in charge of the replication of the data items that fall within its range. In addition to locally storing each key within its range, the coordinator replicates these keys at the N-1 clockwise successor nodes in the ring.

برای دستیابی به در دسترس بودن بالا و پایداری، Dynamo داده‌های خود را بر چندین میزبان تکرار می‌کند. هر قلم داده در N میزبان تکرار می‌شود، جایی که N پارامتری است که "بر اساس نمونه" پیکربندی می‌شود. هر کلید k به یک گره هماهنگ‌کننده تخصیص داده می‌شود. هماهنگ‌کننده مسئول تکرار اشیای داده‌ای است که در بازه آن قرار دارند. علاوه بر ذخیره محلی هر کلید در بازه خود، هماهنگ‌کننده این کلیدها را در N-1 گره جانشین در جهت عقربه ساعت در حلقه تکرار می‌کند.

> The list of nodes that is responsible for storing a particular key is called the preference list. The system is designed so that every node in the system can determine which nodes should be in this list for any particular key. To account for node failures, preference list contains more than N nodes.

فهرست گره‌هایی که مسئول ذخیره یک کلید خاص هستند فهرست ترجیحی نامیده می‌شود. سیستم به گونه‌ای طراحی شده است که هر گره در سیستم می‌تواند تعیین کند که چه گره‌هایی باید در این فهرست برای هر کلید خاص باشند. برای در نظر گرفتن خرابی‌های گره، فهرست ترجیحی شامل بیش از N گره است.

### ۴.۴ نسخه‌بندی داده

> Dynamo provides eventual consistency, which allows for updates to be propagated to all replicas asynchronously. A put() call may return to its caller before the update has been applied at all the replicas, which can result in scenarios where a subsequent get() operation may return an object that does not have the latest updates.

Dynamo سازگاری نهایی را ارائه می‌دهد که اجازه می‌دهد به‌روزرسانی‌ها به صورت ناهمزمان به تمام نسخه‌ها منتشر شوند. فراخوان put() ممکن است قبل از اعمال به‌روزرسانی در تمام نسخه‌ها به فراخواننده خود بازگردد که می‌تواند منجر به سناریوهایی شود که در آنها عملیات get() بعدی شیئی را برمی‌گرداند که جدیدترین به‌روزرسانی‌ها را ندارد.

> There is a category of applications in Amazon's platform that can tolerate such inconsistencies and can be constructed to operate under these conditions. For example, the shopping cart application requires that an "Add to Cart" operation can never be forgotten or rejected.

دسته‌ای از برنامه‌های کاربردی در پلتفرم آمازون وجود دارند که می‌توانند چنین ناسازگاری‌هایی را تحمل کنند و می‌توانند برای عمل کردن تحت این شرایط ساخته شوند. به عنوان مثال، برنامه کاربردی سبد خرید نیاز دارد که عملیات "افزودن به سبد" هرگز فراموش یا رد نشود.

> In order to provide this kind of guarantee, Dynamo treats the result of each modification as a new and immutable version of the data. It allows for multiple versions of an object to be present in the system at the same time. Most of the time, new versions subsume the previous version(s), and the system itself can determine the authoritative version (syntactic reconciliation). However, version branching may happen, in the presence of failures combined with concurrent updates, resulting in conflicting versions of an object.

برای ارائه این نوع تضمین، Dynamo نتیجه هر اصلاح را به عنوان نسخه جدید و تغییرناپذیر داده در نظر می‌گیرد. این اجازه می‌دهد چندین نسخه از یک شیء در سیستم به طور همزمان وجود داشته باشند. بیشتر اوقات، نسخه‌های جدید نسخه(های) قبلی را در بر می‌گیرند و خود سیستم می‌تواند نسخه معتبر را تعیین کند (سازگاری نحوی). با این حال، شاخه‌بندی نسخه ممکن است در حضور خرابی‌ها همراه با به‌روزرسانی‌های همزمان رخ دهد که منجر به نسخه‌های متعارض یک شیء می‌شود.

> Dynamo uses vector clocks in order to capture causality between different versions of the same object. A vector clock is effectively a list of (node, counter) pairs. One vector clock is associated with every version of every object. One can determine whether two versions of an object are on parallel branches or have a causal ordering, by examine their vector clocks.

Dynamo از ساعت‌های برداری برای ثبت روابط علی بین نسخه‌های مختلف یک شیء استفاده می‌کند. ساعت برداری در واقع فهرستی از جفت‌های (گره، شمارنده) است. یک ساعت برداری با هر نسخه از هر شیء مرتبط است. می‌توان با بررسی ساعت‌های برداری آنها تعیین کرد که آیا دو نسخه از یک شیء در شاخه‌های موازی هستند یا ترتیب علی دارند.

### ۴.۵ اجرای عملیات get() و put()

> Both get and put operations are invoked using Amazon's infrastructure-specific request processing framework over HTTP. There are two strategies that a client can use to select a node: (1) route its request through a generic load balancer that will select a node based on load information, or (2) use a partition-aware client library that routes requests directly to the appropriate coordinator nodes.

هر دو عملیات get و put با استفاده از چارچوب پردازش درخواست اختصاصی زیرساخت آمازون از طریق HTTP فراخوانی می‌شوند. دو استراتژی وجود دارد که یک مشتری می‌تواند برای انتخاب گره استفاده کند: (۱) درخواست خود را از طریق یک بالانسر بار عمومی مسیریابی کند که یک گره را بر اساس اطلاعات بار انتخاب می‌کند، یا (۲) از کتابخانه مشتری آگاه به پارتیشن استفاده کند که درخواست‌ها را مستقیماً به گره‌های هماهنگ‌کننده مناسب مسیریابی می‌کند.

> To maintain consistency among its replicas, Dynamo uses a consistency protocol similar to those used in quorum systems. This protocol has two key configurable values: R and W. R is the minimum number of nodes that must participate in a successful read operation. W is the minimum number of nodes that must participate in a successful write operation. Setting R and W such that R + W > N yields a quorum-like system.

برای حفظ سازگاری بین نسخه‌های خود، Dynamo از پروتکل سازگاری مشابه با موارد استفاده شده در سیستم‌های کوروم استفاده می‌کند. این پروتکل دو مقدار پیکربندی کلیدی دارد: R و W. R تعداد حداقل گره‌هایی است که باید در یک عملیات خواندن موفق شرکت کنند. W تعداد حداقل گره‌هایی است که باید در یک عملیات نوشتن موفق شرکت کنند. تنظیم R و W به گونه‌ای که R + W > N باشد، یک سیستم مشابه کوروم ایجاد می‌کند.

### ۴.۶ مدیریت خرابی‌ها: Handoff با اشاره (Hinted Handoff)

> If Dynamo used a traditional quorum approach it would be unavailable during server failures and network partitions, and would have reduced durability even under the simplest of failure conditions. To remedy this it does not enforce strict quorum membership and instead it uses a "sloppy quorum"; all read and write operations are performed on the first N healthy nodes from the preference list.

اگر Dynamo از رویکرد سنتی کوروم استفاده می‌کرد، در حین خرابی سرورها و پارتیشن‌های شبکه در دسترس نبود و حتی تحت ساده‌ترین شرایط خرابی، پایداری کاهش می‌یافت. برای جبران این موضوع، عضویت کوروم سختگیرانه را اعمال نمی‌کند و در عوض از یک "کوروم شل" استفاده می‌کند؛ تمام عملیات خواندن و نوشتن بر اولین N گره سالم از فهرست ترجیحی انجام می‌شوند.

> Consider the example of Dynamo configuration with N=3. If node A is temporarily down or unreachable during a write operation then a replica that would normally have lived on A will now be sent to node D. The replica sent to D will have a hint in its metadata that suggests which node was the intended recipient of the replica. Nodes that receive hinted replicas will keep them in a separate local database that is scanned periodically. Upon detecting that A has recovered, D will attempt to deliver the replica to A.

مثال پیکربندی Dynamo با N=3 را در نظر بگیرید. اگر گره A به طور موقت خراب یا در دسترس نباشد در حین یک عملیات نوشتن، نسخه‌ای که معمولاً در A زندگی می‌کرد现在 به گره D ارسال می‌شود. نسخه ارسال شده به D دارای اشاره‌ای در فراداده خود خواهد بود که نشان می‌دهد کدام گره دریافت‌کننده مورد نظر نسخه بوده است. گره‌هایی که نسخه‌های اشاره‌شده را دریافت می‌کنند آنها را در یک پایگاه داده محلی جداگانه نگهداری می‌کنند که به طور دوره‌ای اسکن می‌شود. پس از تشخیص اینکه A بهبود یافته است، D تلاش می‌کند نسخه را به A تحویل دهد.

### ۴.۷ بازیابی از خرابی‌های دائمی: همگام‌سازی نسخه

> To detect the inconsistencies between replicas faster and to minimize the amount of transferred data, Dynamo uses Merkle trees. A Merkle tree is a hash tree where leaves are hashes of the values of individual keys. Parent nodes higher in the tree are hashes of their respective children. The principal advantage of Merkle tree is that each branch of the tree can be checked independently without requiring nodes to download the entire tree or the entire data set.

برای شناسایی سریعتر ناسازگاری‌ها بین نسخه‌ها و به حداقل رساندن مقدار داده‌های منتقل شده، Dynamo از درخت‌های Merkle استفاده می‌کند. درخت Merkle یک درخت هش است که برگ‌های آن هش مقادیر کلیدهای منفرد هستند. گره‌های والد بالاتر در درخت هش فرزندان مربوطه خود هستند. مزیت اصلی درخت Merkle این است که هر شاخه از درخت می‌تواند به طور مستقل بررسی شود بدون اینکه نیاز باشد گره‌ها کل درخت یا کل مجموعه داده را دانلود کنند.

> Dynamo uses Merkle trees for anti-entropy as follows: Each node maintains a separate Merkle tree for each key range it hosts. This allows nodes to compare whether the keys within a key range are up-to-date.

Dynamo از درخت‌های Merkle برای ضد-آنتروپی به شرح زیر استفاده می‌کند: هر گره یک درخت Merkle جداگانه برای هر بازه کلیدی که میزبانی می‌کند نگهداری می‌کند. این به گره‌ها اجازه می‌دهد مقایسه کنند که آیا کلیدها در یک بازه کلیدی به روز هستند یا خیر.

### ۴.۸ عضویت و تشخیص خرابی

> In Amazon's environment node outages (due to failures and maintenance tasks) are often transient but may last for extended intervals. A node outage rarely signifies a permanent departure and therefore should not result in rebalancing of the partition assignment or repair of the unreachable replicas.

در محیط آمازون، قطعی‌های گره (به دلیل خرابی‌ها و وظایف تعمیر و نگهداری) اغلب موقتی هستند اما ممکن است برای بازه‌های زمانی طولانی ادامه یابند. قطعی یک گره به ندرت نشان‌دهنده خروج دائمی است و بنابراین نباید منجر به بازتوازن تخصیص پارتیشن یا تعمیر نسخه‌های در دسترس نباشد شود.

> To prevent logical partitions, some Dynamo nodes play the role of seeds. Seeds are nodes that are discovered via an external mechanism and are known to all nodes. Because all nodes eventually reconcile their membership with a seed, logical partitions are highly unlikely.

برای جلوگیری از پارتیشن‌های منطقی، برخی از گره‌های Dynamo نقش بذرها را بازی می‌کنند. بذرها گره‌هایی هستند که از طریق مکانیزم خارجی کشف می‌شوند و توسط تمام گره‌ها شناخته شده‌اند. از آنجا که تمام گره‌ها در نهایت عضویت خود را با یک بذر هماهنگ می‌کنند، پارتیشن‌های منطقی بسیار بعید هستند.

> Failure detection in Dynamo is used to avoid attempts to communicate with unreachable peers during get() and put() operations. For the purpose of avoiding failed attempts at communication, a purely local notion of failure detection is entirely sufficient: node A may consider node B failed if node B does not respond to node A's messages.

تشخیص خرابی در Dynamo برای جلوگیری از تلاش‌های ارتباط با همتاهای در دسترس نباشد در حین عملیات get() و put() استفاده می‌شود. برای جلوگیری از تلاش‌های ناموفق ارتباط، مفهوم کاملاً محلی تشخیص خرابی کاملاً کافی است: گره A ممکن است گره B را خراب در نظر بگیرد اگر گره B به پیام‌های گره A پاسخ ندهد.

---

## ۶. تجربیات و درس‌های آموخته شده

> Dynamo is used by several services with different configurations. The following are the main patterns in which Dynamo is used:
> - **Business logic specific reconciliation:** This is a popular use case for Dynamo. Each data object is replicated across multiple nodes. In case of divergent versions, the client application performs its own reconciliation logic.
> - **Timestamp based reconciliation:** This case differs from the previous one only in the reconciliation mechanism. In case of divergent versions, Dynamo performs simple timestamp based reconciliation logic of "last write wins".
> - **High performance read engine:** While Dynamo is built to be an "always writeable" data store, a few services are tuning its quorum characteristics and using it as a high performance read engine.

Dynamo توسط سرویس‌های متعددی با پیکربندی‌های مختلف استفاده می‌شود. الگوهای اصلی که Dynamo در آنها استفاده می‌شود عبارتند از:
- **حل تائم مبتنی بر منطق تجاری:** این یک مورد استفاده محبوب برای Dynamo است. هر شیء داده در چندین گره تکرار می‌شود. در صورت نسخه‌های واگرا، برنامه کاربردی مشتری منطق تائم خود را اجرا می‌کند.
- **حل تائم مبتنی بر برچسب زمانی:** این مورد فقط از نظر مکانیزم حل تائم با مورد قبلی متفاوت است. در صورت نسخه‌های واگرا، Dynamo منطق حل تائم ساده مبتنی بر برچسب زمانی "آخرین نوشتن برنده است" را اجرا می‌کند.
- **موتور خواندن با عملکرد بالا:** در حالی که Dynamo برای یک فروشگاه داده "همیشه قابل نوشتن" ساخته شده است، چند سرویس ویژگی‌های کوروم آن را تنظیم می‌کنند و از آن به عنوان یک موتور خواندن با عملکرد بالا استفاده می‌کنند.

> The main advantage of Dynamo is that its client applications can tune the values of N, R and W to achieve their desired levels of performance, availability and durability. For instance, the value of N determines the durability of each object. A typical value of N used by Dynamo's users is 3.

مزیت اصلی Dynamo این است که برنامه‌های کاربردی مشتری آن می‌توانند مقادیر N، R و W را برای دستیابی به سطوح مطلوب عملکرد، در دسترس بودن و پایداری تنظیم کنند. به عنوان مثال، مقدار N پایداری هر شیء را تعیین می‌کند. مقدار معمول N که توسط کاربران Dynamo استفاده می‌شود ۳ است.

> The values of W and R impact object availability, durability and consistency. For instance, if W is set to 1, then the system will never reject a write request as long as there is at least one node in the system that can successfully process a write request. However, low values of W and R can increase the risk of inconsistency.

مقادیر W و R بر در دسترس بودن، پایداری و سازگاری شیء تأثیر می‌گذارند. به عنوان مثال، اگر W روی ۱ تنظیم شود، سیستم هرگز درخواست نوشتن را رد نمی‌کند تا زمانی که حداقل یک گره در سیستم وجود داشته باشد که بتواند با موفقیت درخواست نوشتن را پردازش کند. با این حال، مقادیر پایین W و R می‌توانند خطر ناسازگاری را افزایش دهند.

> While Dynamo's principle design goal is to build a highly available data store, performance is an equally important criterion in Amazon's platform. A typical SLA required of services that use Dynamo is that 99.9% of the read and write requests execute within 300ms.

در حالی که هدف اصلی طراحی Dynamo ساخت یک فروشگاه داده بسیار در دسترس است، عملکرد معیاری به همان اندازه مهم در پلتفرم آمازون است. یک SLA معمولی که از سرویس‌های استفاده کننده از Dynamo مورد نیاز است این است که ۹۹.۹٪ از درخواست‌های خواندن و نوشتن ظرف ۳۰۰ میلی‌ثانیه اجرا شوند.

> This optimization has resulted in lowering the 99.9th percentile latency by a factor of 5 during peak traffic even for a very small buffer of a thousand objects. Also, write buffering smoothes out higher percentile latencies.

این بهینه‌سازی منجر به کاهش تأخیر صدک ۹۹.۹ به میزان ۵ برابر در ترافیک اوج حتی برای بافر بسیار کوچک هزار شیء شده است. همچنین، بافر نوشتن تأخیرهای صدک بالاتر را هموار می‌کند.

> The production use of Dynamo for the past year demonstrates that decentralized techniques can be combined to provide a single highly-available system. Its success in one of the most challenging application environments shows that an eventual-consistent storage system can be a building block for highly-available applications.

استفاده تولیدی Dynamo در سال گذشته نشان می‌دهد که تکنیک‌های غیرمتمرکز می‌توانند ترکیب شوند تا یک سیستم بسیار در دسترس واحد ارائه دهند. موفقیت آن در یکی از چالش‌برانگیزترین محیط‌های برنامه کاربردی نشان می‌دهد که یک سیستم ذخیره‌سازی سازگار نهایی می‌تواند بلوک سازنده‌ای برای برنامه‌های کاربردی بسیار در دسترس باشد.

---

## یادداشت شخصی

> **اهمیت این مقاله در سیستم‌دیزاین:**
> مقاله Dynamo یکی از مهم‌ترین مقالات در حوزه سیستم‌های توزیع شده است و مفاهیم کلیدی زیر را معرفی می‌کند:
> 1. **Consistent Hashing** - هشینگ سازگار برای پارتیشن‌بندی داده
> 2. **Virtual Nodes** - گره‌های مجازی برای توزیع بهتر بار
> 3. **Vector Clocks** - ساعت‌های برای ردیابی نسخه‌ها و حل تعارض
> 4. **Hinted Handoff** - تحمل خرابی‌های موقت با نگهداری نسخه‌های اشاره شده
> 5. **Merkle Trees** - درخت‌های Merkle برای همگام‌سازی و تشخیص ناسازگاری
> 6. **Quorum (N, R, W)** - مدل کوروم با قابلیت تنظیم بر اساس نیاز
> 7. **Anti-entropy** - پروتکل ضد-آنتروپی برای بازیابی خرابی‌های دائمی

> **ارتباط با فصل ۵ کتاب:**
> مفاهیم Consistent Hashing و Virtual Nodes که در فصل ۵ کتاب توضیح داده شدند، دقیقاً همان تکنیک‌هایی هستند که Dynamo از آنها استفاده می‌کند. این مقاله نشان می‌دهد که چگونه این مفاهیم در یک سیستم واقعی و تولیدی در مقیاس آمازون به کار گرفته شده‌اند.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Dynamo Paper (PDF)](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)
