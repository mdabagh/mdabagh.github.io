> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۶

> **CHAPTER 1:** Designing a system that supports millions of users is challenging, and it is a journey that requires continuous refinement and endless improvement. In this chapter, we build a system that supports a single user and gradually scale it up to serve millions of users. After reading this chapter, you will master a handful of techniques that will help you to crack the system design interview questions.

**فصل ۱:** طراحی سیستمی که بتواند از **میلیون‌ها کاربر** پشتیبانی کند، کاری پیچیده و چالش‌برانگیز است. رسیدن به چنین سیستمی یک فرایند تدریجی است که به **بهبود مستمر (Continuous Refinement)** و **توسعه‌ی پیوسته (Continuous Improvement)** نیاز دارد.

در این فصل، طراحی را از یک سیستم بسیار ساده که تنها از **یک کاربر** پشتیبانی می‌کند آغاز می‌کنیم و سپس آن را قدم‌به‌قدم گسترش می‌دهیم تا بتواند به **میلیون‌ها کاربر** سرویس ارائه دهد.

در پایان این فصل، با مجموعه‌ای از تکنیک‌ها و مفاهیم کلیدی **System Design** آشنا خواهید شد که در پاسخ‌گویی به سؤالات مصاحبه‌های طراحی سیستم، کمک شایانی به شما خواهند کرد.

---

###### 📄 صفحه ۶

> **Single server setup:** A journey of a thousand miles begins with a single step, and building a complex system is no different. To start with something simple, everything is running on a single server. Figure 1-1 shows the illustration of a single server setup where everything is running on one server: web app, database, cache, etc.

**راه‌اندازی تک‌سروری (Single Server Setup):** همان‌طور که ضرب‌المثل معروف می‌گوید: **«سفر هزار فرسخی با اولین قدم آغاز می‌شود.»** طراحی یک سیستم پیچیده نیز از همین اصل پیروی می‌کند.

برای شروع، همه‌ی اجزای سیستم روی **یک سرور** اجرا می‌شوند؛ از جمله:

- برنامه‌ی وب (Web Application)
- پایگاه داده (Database)
- کش (Cache)
- و سایر سرویس‌های موردنیاز

شکل **۱-۱** نمونه‌ای از این معماری را نشان می‌دهد که در آن تمام اجزای سیستم روی یک سرور اجرا می‌شوند.

![Figure 1-1](design-system/images/System-Design-Interview-page6-image1.jpg)

---

###### 📄 صفحه ۶

> **Single server setup:** To understand this setup, it is helpful to investigate the request flow and traffic source. Let us first look at the request flow (Figure 1-2).

برای درک بهتر این معماری، ابتدا لازم است **جریان پردازش درخواست‌ها (Request Flow)** و **منابع تولید ترافیک (Traffic Source)** را بررسی کنیم.

ابتدا به **جریان پردازش درخواست‌ها** می‌پردازیم که در شکل **۱-۲** نمایش داده شده است.

![Figure 1-2](design-system/images/System-Design-Interview-page6-image2.jpg)




---



###### 📄 صفحه ۷

> 1. Users access websites through domain names, such as api.mysite.com. Usually, the Domain Name System (DNS) is a paid service provided by 3rd parties and not hosted by our servers.
> 2. Internet Protocol (IP) address is returned to the browser or mobile app. In the example, IP address 15.125.23.214 is returned.
> 3. Once the IP address is obtained, Hypertext Transfer Protocol (HTTP) [1] requests are sent directly to your web server.
> 4. The web server returns HTML pages or JSON response for rendering.
>
> Next, let us examine the traffic source. The traffic to your web server comes from two sources: web application and mobile application.
>
> - **Web application:** it uses a combination of server-side languages (Java, Python, etc.) to handle business logic, storage, etc., and client-side languages (HTML and JavaScript) for presentation.
> - **Mobile application:** HTTP protocol is the communication protocol between the mobile app and the web server. JavaScript Object Notation (JSON) is commonly used API response format to transfer data due to its simplicity. An example of the API response in JSON format is shown below:

```
GET /users/12 - Retrieve user object for id = 12

{
  "id": 12,
  "firstName": "John",
  "lastName": "Smith",
  "address": {
    "streetAddress": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postalCode": 10021
  },
  "phoneNumbers": [
    "212 555-1234",
    "646 555-4567"
  ]
}
```

کاربر برای دسترسی به وب‌سایت، ابتدا نام دامنه‌ای مانند `api.mysite.com` را وارد می‌کند. معمولاً سرویس **سیستم نام دامنه (DNS)** توسط شرکت‌های شخص ثالث ارائه می‌شود و روی سرورهای ما میزبانی نمی‌شود.

پس از آن، DNS آدرس **IP** مربوط به دامنه را به مرورگر یا اپلیکیشن موبایل بازمی‌گرداند. در این مثال، آدرس `15.125.23.214` برگردانده می‌شود.

مرورگر یا اپلیکیشن موبایل پس از دریافت آدرس IP، درخواست‌های **HTTP (Hypertext Transfer Protocol)** را مستقیماً به وب‌سرور ارسال می‌کند.

در نهایت، وب‌سرور درخواست را پردازش کرده و در پاسخ، صفحات **HTML** یا داده‌های **JSON** را برای نمایش به کاربر ارسال می‌کند.

در ادامه، منبع ترافیک ورودی به وب‌سرور را بررسی می‌کنیم. به‌طور کلی، این ترافیک از دو منبع اصلی تأمین می‌شود:

- **اپلیکیشن وب (Web Application):** برای پیاده‌سازی منطق کسب‌وکار، مدیریت داده‌ها و سایر پردازش‌های سمت سرور از زبان‌هایی مانند **Java** و **Python** استفاده می‌شود. در سمت کاربر نیز رابط کاربری با استفاده از **HTML** و **JavaScript** نمایش داده می‌شود.

- **اپلیکیشن موبایل (Mobile Application):** ارتباط بین اپلیکیشن موبایل و وب‌سرور از طریق پروتکل **HTTP** انجام می‌شود. همچنین **JSON (JavaScript Object Notation)** به دلیل ساختار ساده و سبک خود، رایج‌ترین قالب پاسخ API برای انتقال داده بین سرور و اپلیکیشن است. نمونه‌ای از پاسخ API در قالب JSON در بالا نمایش داده شده است.

---

###### 📄 صفحه ۸

> **Database:** With the growth of the user base, one server is not enough, and we need multiple servers: one for web/mobile traffic, the other for the database (Figure 1-3). Separating web/mobile traffic (web tier) and database (data tier) servers allows them to be scaled independently.

با افزایش تعداد کاربران، استفاده از تنها **یک سرور** دیگر پاسخ‌گوی نیاز سیستم نخواهد بود. در این مرحله، معماری سیستم به چند سرور تقسیم می‌شود؛ یک سرور وظیفه‌ی پردازش درخواست‌های **وب و موبایل (Web Tier)** را بر عهده دارد و سرور دیگری مسئول **پایگاه داده (Data Tier)** است.

جدا کردن **لایه‌ی وب** از **لایه‌ی داده** این امکان را فراهم می‌کند که هر بخش به‌صورت مستقل مقیاس‌پذیر (Scalable) باشد. به بیان دیگر، در صورت افزایش بار روی یکی از این بخش‌ها، می‌توان تنها همان بخش را ارتقا داد، بدون آنکه نیازی به افزایش منابع بخش دیگر باشد.

![Figure 1-3](design-system/images/System-Design-Interview-page8-image1.jpg)





---

###### 📄 صفحه ۸

> **Which databases to use?** You can choose between a traditional relational database and a non-relational database. Let us examine their differences.
>
> Relational databases are also called a relational database management system (RDBMS) or SQL database. The most popular ones are MySQL, Oracle database, PostgreSQL, etc. Relational databases represent and store data in tables and rows. You can perform join operations using SQL across different database tables.
>
> Non-Relational databases are also called NoSQL databases. Popular ones are CouchDB, Neo4j, Cassandra, HBase, Amazon DynamoDB, etc. [2]. These databases are grouped into four categories: key-value stores, graph stores, column stores, and document stores. Join operations are generally not supported in non-relational databases.
>
> For most developers, relational databases are the best option because they have been around for over 40 years and historically, they have worked well. However, if relational databases are not suitable for your specific use cases, it is critical to explore beyond relational databases. Non-relational databases might be the right choice if:
>
> - Your application requires super-low latency.
> - Your data are unstructured, or you do not have any relational data.
> - You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
> - You need to store a massive amount of data.

انتخاب بین یک **پایگاه داده رابطه‌ای (Relational Database)** و یک **پایگاه داده غیررابطه‌ای (Non-Relational Database)**، یکی از تصمیم‌های مهم در طراحی سیستم است. ابتدا تفاوت این دو را بررسی می‌کنیم.

پایگاه‌های داده رابطه‌ای که با نام **سیستم مدیریت پایگاه داده رابطه‌ای (RDBMS)** یا **SQL Database** نیز شناخته می‌شوند، داده‌ها را در قالب **جدول (Table)** و **سطر (Row)** ذخیره می‌کنند. از محبوب‌ترین نمونه‌های آن می‌توان به **MySQL**، **Oracle Database** و **PostgreSQL** اشاره کرد. یکی از مهم‌ترین قابلیت‌های این نوع پایگاه داده، اجرای عملیات **JOIN** با استفاده از زبان **SQL** برای ترکیب داده‌های چند جدول است.

در مقابل، پایگاه‌های داده غیررابطه‌ای که با نام **NoSQL Database** شناخته می‌شوند، شامل نمونه‌هایی مانند **CouchDB**، **Neo4j**، **Cassandra**، **HBase** و **Amazon DynamoDB** هستند. این پایگاه‌های داده معمولاً در چهار گروه اصلی دسته‌بندی می‌شوند:

- Key-Value Store
- Graph Store
- Column Store
- Document Store

برخلاف پایگاه‌های داده رابطه‌ای، در بیشتر پایگاه‌های داده NoSQL عملیات **JOIN** پشتیبانی نمی‌شود.

برای بسیاری از پروژه‌ها، پایگاه‌های داده رابطه‌ای همچنان بهترین انتخاب هستند؛ زیرا بیش از ۴۰ سال است که در صنعت نرم‌افزار استفاده می‌شوند و کارایی خود را ثابت کرده‌اند. بااین‌حال، اگر نیازهای پروژه با ویژگی‌های این نوع پایگاه داده سازگار نباشد، استفاده از **NoSQL** می‌تواند گزینه مناسب‌تری باشد.

پایگاه‌های داده **NoSQL** معمولاً در شرایط زیر انتخاب بهتری هستند:

- زمانی که سیستم به **Latency** بسیار پایین نیاز دارد.
- زمانی که داده‌ها ساختار مشخصی ندارند (**Unstructured Data**) یا ارتباطی بین آن‌ها وجود ندارد.
- زمانی که تنها نیاز به ذخیره و بازیابی داده‌هایی مانند **JSON**، **XML** یا **YAML** دارید.
- زمانی که باید حجم بسیار زیادی از داده ذخیره شود.

---

###### 📄 صفحه ۹

> **Vertical scaling vs horizontal scaling:** Vertical scaling, referred to as "scale up", means the process of adding more power (CPU, RAM, etc.) to your servers. Horizontal scaling, referred to as "scale-out", allows you to scale by adding more servers into your pool of resources.
>
> When traffic is low, vertical scaling is a great option, and the simplicity of vertical scaling is its main advantage. Unfortunately, it comes with serious limitations.
>
> - Vertical scaling has a hard limit. It is impossible to add unlimited CPU and memory to a single server.
> - Vertical scaling does not have failover and redundancy. If one server goes down, the website/app goes down with it completely.
>
> Horizontal scaling is more desirable for large scale applications due to the limitations of vertical scaling.
>
> In the previous design, users are connected to the web server directly. Users will unable to access the website if the web server is offline. In another scenario, if many users access the web server simultaneously and it reaches the web server's load limit, users generally experience slower response or fail to connect to the server. A load balancer is the best technique to address these problems.

**مقیاس‌پذیری عمودی (Vertical Scaling)** که با نام **Scale Up** نیز شناخته می‌شود، به معنای افزایش منابع سخت‌افزاری یک سرور، مانند **CPU**، **RAM** و سایر منابع است.

در مقابل، **مقیاس‌پذیری افقی (Horizontal Scaling)** یا **Scale Out** به معنای افزایش ظرفیت سیستم از طریق اضافه کردن سرورهای جدید به مجموعه‌ی سرورها است.

زمانی که میزان ترافیک پایین باشد، مقیاس‌پذیری عمودی انتخاب مناسبی است و سادگی پیاده‌سازی، مهم‌ترین مزیت آن محسوب می‌شود. بااین‌حال، این روش محدودیت‌های مهمی نیز دارد:

- امکان افزایش نامحدود منابع سخت‌افزاری یک سرور وجود ندارد و هر سرور سقف مشخصی برای CPU و حافظه دارد.
- در این روش مکانیزم **Failover** و **Redundancy** وجود ندارد؛ بنابراین اگر همان سرور از دسترس خارج شود، کل وب‌سایت یا اپلیکیشن نیز از کار خواهد افتاد.

به دلیل همین محدودیت‌ها، **مقیاس‌پذیری افقی** برای سیستم‌های بزرگ و پرترافیک گزینه مناسب‌تری محسوب می‌شود.

در معماری قبلی، کاربران مستقیماً به وب‌سرور متصل می‌شدند. بنابراین اگر وب‌سرور از دسترس خارج می‌شد، کاربران دیگر نمی‌توانستند به وب‌سایت دسترسی داشته باشند.

از سوی دیگر، اگر تعداد زیادی کاربر به‌صورت هم‌زمان درخواست ارسال می‌کردند و بار سرور از ظرفیت آن فراتر می‌رفت، کاربران با افزایش زمان پاسخ‌گویی یا حتی قطع ارتباط با سرور مواجه می‌شدند.

راهکار استاندارد برای حل این مشکلات، استفاده از **Load Balancer** است که درخواست‌های ورودی را بین چندین وب‌سرور توزیع می‌کند.



---






###### 📄 صفحه ۱۰

> **Load balancer** A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set. Figure 1-4 shows how a load balancer works

یک **بالانسر بار (Load Balancer)** ترافیک ورودی را به‌طور یکنواخت بین سرورهای وبی که در یک مجموعه‌ی بالانس‌شده (load-balanced set) تعریف شده‌اند، توزیع می‌کند. شکل ۱-۴ نحوه‌ی عملکرد یک بالانسر بار را نشان می‌دهد.

![Figure 1-4](design-system/images/System-Design-Interview-page10-image1.jpg)

---

>  As shown in Figure 1-4, users connect to the public IP of the load balancer directly. With this setup, web servers are unreachable directly by clients anymore. For better   security, private IPs are used for communication between servers. A private IP is an IP address reachable only between servers in the same network; however, it is unreachable >  over the internet. The load balancer communicates with web servers through private IPs.
>  In Figure 1-4, after a load balancer and a second web server are added, we successfully solved no failover issue and improved the availability of the web tier. Details are >  explained below:
>  • If server 1 goes offline, all the traffic will be routed to server 2. This prevents the website from going offline. We will also add a new healthy web server to the server >  pool to balance the load.
>  • If the website traffic grows rapidly, and two servers are not enough to handle the traffic, the load balancer can handle this problem gracefully. You only need to add more >  servers to the web server pool, and the load balancer automatically starts to send requests to them.
>  Now the web tier looks good, what about the data tier? The current design has one database, so it does not support failover and redundancy. Database replication is a common >  technique to address those problems. Let us take a look.


### نحوه‌ی عملکرد بالانسر بار
همان‌طور که در شکل ۱-۴ نشان داده شده، کاربران مستقیماً به IP عمومی (public IP) بالانسر بار متصل می‌شوند. با این ساختار، سرورهای وب دیگر به‌طور مستقیم توسط کلاینت‌ها قابل دسترسی نیستند. برای امنیت بیشتر، از IPهای خصوصی (private IP) برای ارتباط بین سرورها استفاده می‌شود. IP خصوصی، آدرسی است که فقط بین سرورهای داخل یک شبکه‌ی یکسان قابل دسترسی است و از طریق اینترنت قابل‌دسترس نیست. بالانسر بار از طریق IPهای خصوصی با سرورهای وب ارتباط برقرار می‌کند.

در شکل ۱-۴، پس از اضافه شدن یک بالانسر بار و یک سرور وب دوم، مشکل نبود failover برطرف شده و در دسترس‌بودن (availability) لایه‌ی وب بهبود یافته است. جزئیات آن به شرح زیر است:

- اگر سرور ۱ آفلاین شود، تمام ترافیک به سرور ۲ هدایت می‌شود. این کار مانع از آفلاین‌شدن کامل وب‌سایت می‌شود. همچنین یک سرور وب سالم جدید نیز به مجموعه‌ی سرورها اضافه می‌شود تا بار (load) به‌درستی توزیع شود.
- اگر ترافیک وب‌سایت به‌سرعت افزایش یابد و دو سرور برای مدیریت آن کافی نباشند، بالانسر بار می‌تواند این مشکل را به‌خوبی مدیریت کند. کافی است سرورهای بیشتری به مجموعه‌ی سرورهای وب اضافه شود؛ بالانسر بار به‌طور خودکار شروع به ارسال درخواست‌ها به آن‌ها می‌کند.

حالا که لایه‌ی وب وضعیت خوبی دارد، وضعیت لایه‌ی داده چطور است؟ طراحی فعلی تنها یک پایگاه داده دارد، پس از failover و افزونگی (redundancy) پشتیبانی نمی‌کند. **همانندسازی پایگاه داده (Database Replication)** تکنیکی رایج برای رفع این مشکلات است. در ادامه به بررسی آن می‌پردازیم.


---

###### 📄 صفحه ۱۲


>  **Database replication**
>  Quoted from Wikipedia: "Database replication can be used in many database management systems, usually with a master/slave relationship between the original (master) and the >  copies (slaves)" [3].
>  A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations. All the   data-modifying commands like insert, delete, or update must be sent to the master database. Most applications require a much higher ratio of reads to writes; thus, the number >  of slave databases in a system is usually larger than the number of master databases. Figure 1-5 shows a master database with multiple slave databases.



### همانندسازی پایگاه داده (Database Replication)

به‌نقل از ویکی‌پدیا: "همانندسازی پایگاه داده می‌تواند در بسیاری از سیستم‌های مدیریت پایگاه داده استفاده شود، معمولاً با یک رابطه‌ی مستر/اسلیو بین نسخه‌ی اصلی (master) و کپی‌ها (slave)".

یک پایگاه داده‌ی master معمولاً فقط از عملیات نوشتن (write) پشتیبانی می‌کند. یک پایگاه داده‌ی slave، کپی‌هایی از داده را از پایگاه داده‌ی master دریافت می‌کند و فقط از عملیات خواندن (read) پشتیبانی می‌کند. تمام دستورات تغییردهنده‌ی داده مانند insert، delete یا update باید به پایگاه داده‌ی master ارسال شوند. اکثر اپلیکیشن‌ها به نسبت بسیار بالاتری از عملیات خواندن نسبت به نوشتن نیاز دارند؛ به همین دلیل، تعداد پایگاه‌های داده‌ی slave در یک سیستم معمولاً بیشتر از تعداد پایگاه‌های داده‌ی master است. شکل ۱-۵ یک پایگاه داده‌ی master به همراه چند پایگاه داده‌ی slave را نشان می‌دهد.


![Figure 1-5](design-system/images/System-Design-Interview-page12-image1.jpg)








---


###### 📄 صفحه ۱۴

>  Advantages of database replication:
>  • Better performance: In the master-slave model, all writes and updates happen in master nodes; whereas, read operations are distributed across slave nodes. This model improves   performance because it allows more queries to be processed in parallel.
>  • Reliability: If one of your database servers is destroyed by a natural disaster, such as a typhoon or an earthquake, data is still preserved. You do not need to worry about >  data loss because data is replicated across multiple locations.
>  • High availability: By replicating data across different locations, your website remains in operation even if a database is offline as you can access data stored in another >  database server.
>  In the previous section, we discussed how a load balancer helped to improve system availability. We ask the same question here: what if one of the databases goes offline? The >  architectural design discussed in Figure 1-5 can handle this case:
>  • If only one slave database is available and it goes offline, read operations will be directed to the master database temporarily. As soon as the issue is found, a new slave >  database will replace the old one. In case multiple slave databases are available, read operations are redirected to other healthy slave databases. A new database server will   replace the old one.
>  • If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master   database. A new slave database will replace the old one for data replication immediately.
>  In production systems, promoting a new master is more complicated as the data in a slave database might not be up to date. The missing data needs to be updated by running data   recovery scripts. Although some other replication methods like multi-masters and circular replication could help, those setups are more complicated; and their discussions are   beyond the scope of this book. Interested readers should refer to the listed reference materials [4] [5].
>  Figure 1-6 shows the system design after adding the load balancer and database replication.


### مزایای همانندسازی پایگاه داده

- **عملکرد بهتر:** در مدل master-slave، تمام عملیات نوشتن و به‌روزرسانی روی گره‌های master انجام می‌شود؛ در حالی که عملیات خواندن بین گره‌های slave توزیع می‌شود. این مدل عملکرد را بهبود می‌بخشد، چون امکان پردازش موازی تعداد بیشتری کوئری را فراهم می‌کند.
- **قابلیت‌اطمینان (Reliability):** اگر یکی از سرورهای پایگاه داده‌ی شما در اثر یک بلای طبیعی مانند طوفان یا زلزله از بین برود، داده‌ها همچنان حفظ می‌شوند. نیازی نیست نگران از دست رفتن داده باشید، زیرا داده در چند مکان مختلف همانندسازی شده است.
- **در‌دسترس‌بودن بالا (High Availability):** با همانندسازی داده در مکان‌های مختلف، حتی اگر یکی از پایگاه‌های داده آفلاین شود، وب‌سایت شما همچنان فعال می‌ماند، زیرا می‌توانید به داده‌ی ذخیره‌شده در سرور پایگاه داده‌ی دیگر دسترسی داشته باشید.

در بخش قبل بررسی کردیم که چگونه یک بالانسر بار به بهبود در‌دسترس‌بودن سیستم کمک می‌کند. همین سؤال را اینجا هم مطرح می‌کنیم: اگر یکی از پایگاه‌های داده آفلاین شود چه اتفاقی می‌افتد؟ طراحی معماری بررسی‌شده در شکل ۱-۵ می‌تواند این حالت را مدیریت کند:

- اگر فقط یک پایگاه داده‌ی slave در دسترس باشد و آفلاین شود، عملیات خواندن به‌طور موقت به پایگاه داده‌ی master هدایت می‌شود. به‌محض شناسایی مشکل، یک پایگاه داده‌ی slave جدید جایگزین قبلی می‌شود. در صورتی که چند پایگاه داده‌ی slave در دسترس باشند، عملیات خواندن به سایر پایگاه‌های داده‌ی سالم هدایت می‌شود و یک سرور جدید جایگزین سرور قبلی خواهد شد.
- اگر پایگاه داده‌ی master آفلاین شود، یکی از پایگاه‌های داده‌ی slave به‌عنوان master جدید ترفیع (promote) می‌یابد. تمام عملیات پایگاه داده به‌طور موقت روی master جدید اجرا می‌شود و بلافاصله یک slave جدید برای همانندسازی داده جایگزین قبلی می‌شود.

در سیستم‌های واقعی (production)، ترفیع یک master جدید پیچیده‌تر است، زیرا ممکن است داده‌ی موجود در پایگاه داده‌ی slave به‌روز نباشد. داده‌های ازدست‌رفته باید با اجرای اسکریپت‌های بازیابی داده (data recovery scripts) به‌روزرسانی شوند. اگرچه روش‌های همانندسازی دیگری مانند multi-master و circular replication نیز می‌توانند کمک‌کننده باشند، اما راه‌اندازی آن‌ها پیچیده‌تر است و بررسی آن‌ها خارج از محدوده‌ی این کتاب است. خوانندگان علاقه‌مند می‌توانند به منابع مرجع ذکرشده مراجعه کنند [۴][۵].

> ***یادداشت شخصی***
>
> در مورد Replication بیشتر تحقیق کن: تفاوت‌های Synchronous Replication و Asynchronous Replication چیست، و هرکدام چطور در عمل پیاده‌سازی می‌شوند؟
>
> [مستندات رسمی Replication در Galera Cluster](https://mariadb.com/docs/galera-cluster/readme/about-galera-replication)
>
> [راهنمای جامع کلاسترینگ Galera در MariaDB](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=GaleraReplication)

شکل ۱-۶ طراحی سیستم پس از افزودن بالانسر بار و همانندسازی پایگاه داده را نشان می‌دهد (صفحه ۱۴).

![Figure 1-6](design-system/images/System-Design-Interview-page14-image1.jpg)




---

>  **Let us take a look at the design:**
>  • A user gets the IP address of the load balancer from DNS.
>  • A user connects the load balancer with this IP address.
>  • The HTTP request is routed to either Server 1 or Server 2.
>  • A web server reads user data from a slave database.
>  • A web server routes any data-modifying operations to the master database. This includes write, update, and delete operations.
>  Now, you have a solid understanding of the web and data tiers, it is time to improve the load/response time. This can be done by adding a cache layer and shifting static   content (JavaScript/CSS/image/video files) to the content delivery network (CDN).


### بررسی طراحی نهایی

بیایید نگاهی به این طراحی بیندازیم:

- کاربر آدرس IP بالانسر بار را از DNS دریافت می‌کند.
- کاربر با استفاده از این آدرس IP به بالانسر بار متصل می‌شود.
- درخواست HTTP به سرور ۱ یا سرور ۲ هدایت می‌شود.
- سرور وب داده‌ی کاربر را از یک پایگاه داده‌ی slave می‌خواند.
- سرور وب هرگونه عملیات تغییردهنده‌ی داده (شامل نوشتن، به‌روزرسانی و حذف) را به پایگاه داده‌ی master هدایت می‌کند.

اکنون که درک خوبی از لایه‌های وب و داده به دست آورده‌اید، وقت آن رسیده که زمان بارگذاری/پاسخ (load/response time) را بهبود دهیم. این کار با افزودن یک لایه‌ی کش (cache) و انتقال محتوای استاتیک (فایل‌های JavaScript/CSS/تصویر/ویدیو) به شبکه‌ی توزیع محتوا (CDN) امکان‌پذیر است.


---

###### 📄 صفحه ۱۵

> **Cache**
> A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly. As illustrated in Figure 1-6, every time a new web page loads, one or more database calls are executed to fetch data. The application performance is greatly affected by calling the database repeatedly. The cache can mitigate this problem.
> ***Cache tier***
> The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently. Figure 1-7 shows a possible setup of a cache server:


### کش (Cache) — صفحه ۱۵

**کش (Cache)** یک ناحیه‌ی ذخیره‌سازی موقت است که نتیجه‌ی پاسخ‌های پرهزینه یا داده‌های پرتکرار را در حافظه ذخیره می‌کند تا درخواست‌های بعدی سریع‌تر پاسخ داده شوند. همان‌طور که در شکل ۱-۶ نشان داده شد، هر بار که یک صفحه‌ی وب جدید بارگذاری می‌شود، یک یا چند فراخوانی پایگاه داده برای دریافت داده اجرا می‌شود. فراخوانی مکرر پایگاه داده تأثیر زیادی بر عملکرد اپلیکیشن دارد. کش می‌تواند این مشکل را کاهش دهد.

### لایه‌ی کش (Cache Tier) — صفحه ۱۵

لایه‌ی کش، یک لایه‌ی ذخیره‌سازی موقت داده است که بسیار سریع‌تر از پایگاه داده عمل می‌کند. مزایای داشتن یک لایه‌ی کش جداگانه شامل بهبود عملکرد سیستم، کاهش بار روی پایگاه داده، و امکان مقیاس‌پذیری مستقل لایه‌ی کش است. شکل ۱-۷ نمونه‌ای از راه‌اندازی یک سرور کش را نشان می‌دهد.

![Figure 1-7](design-system/images/System-Design-Interview-page15-image1.jpg)



---

> After receiving a request, a web server first checks if the cache has the available response. If it has, it sends data back to the client. If not, it queries the database, stores the response in cache, and sends it back to the client. This caching strategy is called a read-through cache. Other caching strategies are available depending on the data type, size, and access patterns. A previous study explains how different caching strategies work [6].
> Interacting with cache servers is simple because most cache servers provide APIs for common programming languages. The following code snippet shows typical Memcached APIs:


# ترجمه

### نحوه‌ی عملکرد کش — صفحه ۱۵

پس از دریافت یک درخواست، سرور وب ابتدا بررسی می‌کند که آیا پاسخ موردنیاز در کش موجود است یا خیر. اگر موجود باشد، داده مستقیماً به کلاینت بازگردانده می‌شود. اگر موجود نباشد، سرور از پایگاه داده کوئری می‌گیرد، پاسخ را در کش ذخیره می‌کند و سپس آن را به کلاینت برمی‌گرداند. این استراتژی کشینگ، **کش خواندن‌محور (Read-Through Cache)** نامیده می‌شود. بسته به نوع داده، اندازه و الگوهای دسترسی، استراتژی‌های کشینگ دیگری نیز وجود دارد که در یک مطالعه‌ی پیشین توضیح داده شده‌اند [۶].

تعامل با سرورهای کش ساده است، زیرا اکثر سرورهای کش برای زبان‌های برنامه‌نویسی رایج، APIهایی ارائه می‌دهند. قطعه‌کد زیر نمونه‌ای از APIهای متداول Memcached را نشان می‌دهد.


![Memcached API example](design-system/images/System-Design-Interview-page15-image2.jpg)



---

###### 📄 صفحه ۱۶


> *Considerations for using cache*
> **Here are a few considerations for using a cache system:**
> • Decide when to use cache. Consider using cache when data is read frequently but modified infrequently. Since cached data is stored in volatile memory, a cache server is not ideal for persisting data. For instance, if a cache server restarts, all the data in memory is lost. Thus, important data should be saved in persistent data stores.
> • Expiration policy. It is a good practice to implement an expiration policy. Once cached data is expired, it is removed from the cache. When there is no expiration policy, cached data will be stored in the memory permanently. It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.
> • Consistency: This involves keeping the data store and the cache in sync. Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction. When scaling across multiple regions, maintaining consistency between the data store and cache is challenging. For further details, refer to the paper titled "Scaling Memcache at Facebook" published by Facebook [7].
> • Mitigating failures: A single cache server represents a potential single point of failure (SPOF), defined in Wikipedia as follows: "A single point of failure (SPOF) is a part of a system that, if it fails, will stop the entire system from working" [8]. As a result, multiple cache servers across different data centers are recommended to avoid SPOF. Another recommended approach is to overprovision the required memory by certain percentages. This provides a buffer as the memory usage increases


### ملاحظات استفاده از کش

در ادامه چند نکته درباره‌ی استفاده از سیستم کش آورده شده است:

- **تصمیم‌گیری درباره‌ی زمان استفاده از کش:** استفاده از کش را برای داده‌هایی در نظر بگیرید که به‌کرات خوانده می‌شوند اما به‌ندرت تغییر می‌کنند. از آنجایی که داده‌ی کش‌شده در حافظه‌ی فرار (volatile memory) ذخیره می‌شود، سرور کش برای نگهداری دائمی داده مناسب نیست. برای مثال، اگر سرور کش ریست شود، تمام داده‌های موجود در حافظه از بین می‌روند. بنابراین، داده‌های مهم باید در فضای ذخیره‌سازی دائمی (persistent data store) نگهداری شوند.
- **سیاست انقضا (Expiration Policy):** پیاده‌سازی یک سیاست انقضا کار درستی است. پس از منقضی‌شدن داده‌ی کش‌شده، از کش حذف می‌شود. در صورت نبود سیاست انقضا، داده‌ی کش‌شده برای همیشه در حافظه باقی می‌ماند. توصیه می‌شود زمان انقضا خیلی کوتاه انتخاب نشود، چون باعث می‌شود سیستم مجبور شود داده را خیلی زیاد از پایگاه داده بارگذاری مجدد کند. از طرف دیگر، بهتر است زمان انقضا خیلی طولانی هم نباشد، چون ممکن است داده قدیمی و نامعتبر (stale) شود.
- **سازگاری (Consistency):** این موضوع به معنای هماهنگ نگه‌داشتن فضای ذخیره‌سازی داده و کش است. ناسازگاری می‌تواند رخ دهد چون عملیات تغییردهنده‌ی داده روی پایگاه داده و کش در یک تراکنش واحد انجام نمی‌شوند. هنگام مقیاس‌پذیری بین چند منطقه‌ی جغرافیایی، حفظ سازگاری بین پایگاه داده و کش چالش‌برانگیز است. برای جزئیات بیشتر، به مقاله‌ی «Scaling Memcache at Facebook» منتشرشده توسط فیسبوک مراجعه کنید [۷].
- **کاهش اثر خرابی‌ها (Mitigating Failures):** یک سرور کش تنها، می‌تواند به‌عنوان یک نقطه‌ی شکست واحد (Single Point of Failure یا SPOF) عمل کند. طبق تعریف ویکی‌پدیا، "نقطه‌ی شکست واحد بخشی از یک سیستم است که اگر از کار بیفتد، کل سیستم را متوقف می‌کند" [۸]. به همین دلیل، استفاده از چند سرور کش در مراکز داده‌ی مختلف برای جلوگیری از SPOF توصیه می‌شود. رویکرد توصیه‌شده‌ی دیگر، اختصاص‌دادن حافظه‌ی بیشتر از میزان موردنیاز (overprovisioning) به میزان درصد مشخصی است. این کار در صورت افزایش مصرف حافظه، یک حاشیه‌ی اطمینان (buffer) ایجاد می‌کند.

![Considerations for using cache](design-system/images/System-Design-Interview-page16-image1.jpg)


---


> Eviction Policy: Once the cache is full, any requests to add items to the cache might cause existing items to be removed. This is called cache eviction. Least-recently-used (LRU) is the most popular cache eviction policy. Other eviction policies, such as the Least Frequently Used (LFU) or First in First Out (FIFO), can be adopted to satisfy different use cases.

### سیاست حذف داده از کش (Eviction Policy)

**سیاست حذف (Eviction Policy):** زمانی که کش پر می‌شود، هر درخواستی برای افزودن آیتم جدید به کش ممکن است باعث حذف آیتم‌های موجود شود. این فرایند **حذف از کش (Cache Eviction)** نامیده می‌شود. **کمترین استفاده‌ی اخیر (Least Recently Used یا LRU)** محبوب‌ترین سیاست حذف کش است. سیاست‌های دیگری مانند **کمترین دفعات استفاده (Least Frequently Used یا LFU)** یا **اولین ورودی، اولین خروجی (First In First Out یا FIFO)** نیز می‌توانند برای برآورده‌کردن نیازهای مختلف مورد استفاده قرار گیرند.



---
###### 📄 صفحه 17



>  **Content delivery network (CDN)**
> A CDN is a network of geographically dispersed servers used to deliver static content. CDN servers cache static content like images, videos, CSS, JavaScript files, etc.Dynamic content caching is a relatively new concept and beyond the scope of this book. It enables the caching of HTML pages that are based on request path, query strings, cookies, and request headers. Refer to the article mentioned in reference material [9] for more about this. This book focuses on how to use CDN to cache static content. Here is how CDN works at the high-level: when a user visits a website, a CDN server closest to the user will deliver static content. Intuitively, the further users are from CDN servers, the slower the website loads. For example, if CDN servers are in San Francisco, users in Los Angeles will get content faster than users in Europe. Figure 1-9 is a great example that shows how CDN improves load time.



### شبکه توزیع محتوا (CDN)

CDN شبکه‌ای از سرورهای پراکنده در نقاط مختلف جغرافیایی است که برای تحویل محتوای استاتیک استفاده می‌شود. سرورهای CDN محتوای استاتیک مانند تصاویر، ویدیوها، فایل‌های CSS، جاوااسکریپت و غیره را کش (ذخیره موقت) می‌کنند. کش کردن محتوای داینامیک مفهومی نسبتاً جدید است و خارج از محدوده این کتاب قرار دارد. این روش امکان کش کردن صفحات HTML را بر اساس مسیر درخواست، رشته‌های کوئری، کوکی‌ها و هدرهای درخواست فراهم می‌کند. برای اطلاعات بیشتر در این زمینه به مرجع شماره [۹] مراجعه کنید. تمرکز این کتاب بر نحوه استفاده از CDN برای کش کردن محتوای استاتیک است.

در سطح بالا، عملکرد CDN به این صورت است: وقتی کاربری از یک وب‌سایت دیدن می‌کند، نزدیک‌ترین سرور CDN به آن کاربر، محتوای استاتیک را تحویل می‌دهد. به‌طور طبیعی، هرچه فاصله کاربران از سرورهای CDN بیشتر باشد، بارگذاری وب‌سایت کندتر خواهد بود. برای مثال، اگر سرورهای CDN در سان‌فرانسیسکو باشند، کاربران در لس‌آنجلس محتوا را سریع‌تر از کاربران در اروپا دریافت می‌کنند. شکل ۱-۹ نمونه‌ی خوبی است که نشان می‌دهد CDN چگونه زمان بارگذاری را بهبود می‌بخشد.

![Content delivery network](design-system/images/System-Design-Interview-page17-image1.jpg)


---

> Figure 1-10 demonstrates the CDN workflow.

شکل ۱-۱۰ روند کار CDN را نشان می‌دهد.

![Content delivery network](design-system/images/System-Design-Interview-page17-image2.jpg)


---

> 1. User A tries to get image.png by using an image URL. The URL’s domain is provided by the CDN provider. The following two image URLs are samples used to demonstrate what image URLs look like on Amazon and Akamai CDNs: 
>  
>  • https://mysite.cloudfront.net/logo.jpg
>  • https://mysite.akamai.com/image-manager/img/logo.jpg
>  2. If the CDN server does not have image.png in the cache, the CDN server requests the file from the origin, which can be a web server or online storage like Amazon S3.
>  3. The origin returns image.png to the CDN server, which includes optional HTTP header Time-to-Live (TTL) which describes how long the image is cached.
> 4. The CDN caches the image and returns it to User A. The image remains cached in the CDN until the TTL expires.
>  5. User B sends a request to get the same image.
>  6. The image is returned from the cache as long as the TTL has not expired.


۱. کاربر A سعی می‌کند تصویر image.png را با استفاده از یک URL تصویر دریافت کند. دامنه‌ی این URL توسط ارائه‌دهنده CDN مشخص شده است. دو نمونه URL زیر برای نشان دادن ظاهر URLهای تصویر در CDNهای آمازون و آکامای آورده شده‌اند:
 • https://mysite.cloudfront.net/logo.jpg
 • https://mysite.akamai.com/image-manager/img/logo.jpg

۲. اگر سرور CDN فایل image.png را در کش نداشته باشد، سرور CDN این فایل را از سرور اصلی (origin) درخواست می‌کند که می‌تواند یک وب‌سرور یا فضای ذخیره‌سازی آنلاین مانند Amazon S3 باشد.

۳. سرور اصلی فایل image.png را به سرور CDN برمی‌گرداند، همراه با هدر HTTP اختیاری Time-to-Live (TTL) که مشخص می‌کند تصویر چه مدت باید کش شود.

۴. سرور CDN تصویر را کش می‌کند و آن را به کاربر A برمی‌گرداند. تصویر تا زمانی که TTL منقضی نشود، در CDN باقی می‌ماند.

۵. کاربر B درخواستی برای دریافت همان تصویر ارسال می‌کند.

۶. تا زمانی که TTL منقضی نشده باشد، تصویر از کش برگردانده می‌شود.


---
## Considerations of using a CDN

> • Cost: CDNs are run by third-party providers, and you are charged for data transfers in and out of the CDN. Caching infrequently used assets provides no significant benefits so you should consider moving them out of the CDN.
>
> • Setting an appropriate cache expiry: For time-sensitive content, setting a cache expiry time is important. The cache expiry time should neither be too long nor too short. If it is too long, the content might no longer be fresh. If it is too short, it can cause repeat reloading of content from origin servers to the CDN.
>
> • CDN fallback: You should consider how your website/application copes with CDN failure. If there is a temporary CDN outage, clients should be able to detect the problem and request resources from the origin.
>
> • Invalidating files: You can remove a file from the CDN before it expires by performing one of the following operations:
>
> • Invalidate the CDN object using APIs provided by CDN vendors.
>
> • Use object versioning to serve a different version of the object. To version an object, you can add a parameter to the URL, such as a version number. For example, version number 2 is added to the query string: image.png?v=2.


### نکات مهم هنگام استفاده از CDN

- **هزینه (Cost):** سرویس‌های CDN توسط شرکت‌های شخص ثالث ارائه می‌شوند و هزینه‌ی انتقال داده به داخل و خارج از CDN از شما دریافت می‌شود. کش کردن فایل‌هایی که به‌ندرت مورد استفاده قرار می‌گیرند، مزیت قابل توجهی ندارد؛ بنابراین بهتر است این نوع فایل‌ها را از CDN خارج کنید.

- **تنظیم مناسب زمان انقضای کش (Cache Expiry):** برای محتوایی که به‌صورت مداوم تغییر می‌کند، انتخاب زمان مناسب برای انقضای کش اهمیت زیادی دارد. این زمان نباید بیش از حد طولانی باشد، زیرا ممکن است کاربران محتوای قدیمی دریافت کنند. همچنین نباید بیش از حد کوتاه باشد، چون باعث می‌شود فایل‌ها مکرراً از سرور اصلی دریافت شده و بار اضافی روی سیستم ایجاد شود.

- **مکانیزم جایگزین در صورت خرابی CDN (CDN Fallback):** باید از قبل مشخص کنید که در صورت از دسترس خارج شدن موقت CDN، وب‌سایت یا اپلیکیشن چگونه رفتار خواهد کرد. در چنین شرایطی، کلاینت‌ها باید بتوانند خرابی CDN را تشخیص داده و فایل‌ها را مستقیماً از سرور اصلی (Origin) دریافت کنند.

- **باطل کردن فایل‌های کش‌شده (Invalidating Files):** در صورت نیاز می‌توانید قبل از پایان یافتن TTL، فایل‌ها را از CDN حذف یا جایگزین کنید. این کار معمولاً به یکی از روش‌های زیر انجام می‌شود:

  - استفاده از APIهای ارائه‌شده توسط سرویس‌دهنده CDN برای **Invalidate** کردن فایل.
  - استفاده از **Object Versioning** و ارائه نسخه جدید فایل. برای این کار معمولاً شماره نسخه به URL اضافه می‌شود. برای مثال:

```text
image.png?v=2
```

---

###### 📄 صفحه 18


> Figure 1-11 shows the design after the CDN and cache are added.

شکل ۱-۱۱ معماری سیستم را پس از اضافه شدن **CDN** و **Cache** نمایش می‌دهد.

---

![Design after CDN and Cache](design-system/images/System-Design-Interview-page18-image1.jpg)

---

> 1. Static assets (JS, CSS, images, etc.,) are no longer served by web servers. They are fetched from the CDN for better performance.
>
> 2. The database load is lightened by caching data.

۱. فایل‌های استاتیک مانند **JavaScript، CSS، تصاویر و سایر Assetها** دیگر مستقیماً توسط وب‌سرورها ارائه نمی‌شوند، بلکه از طریق **CDN** در اختیار کاربران قرار می‌گیرند تا سرعت بارگذاری افزایش یابد.

۲. بار وارد شده به پایگاه داده با استفاده از **Cache** کاهش پیدا می‌کند؛ زیرا داده‌هایی که زیاد درخواست می‌شوند مستقیماً از کش پاسخ داده می‌شوند.

---

# Stateless Web Tier

> Now it is time to consider scaling the web tier horizontally. For this, we need to move state (for instance user session data) out of the web tier. A good practice is to store session data in the persistent storage such as relational database or NoSQL. Each web server in the cluster can access state data from databases. This is called stateless web tier.

اکنون زمان آن رسیده است که **لایه وب (Web Tier)** را به صورت **Horizontal Scaling** گسترش دهیم.

برای انجام این کار، باید **State** (برای مثال اطلاعات Session کاربران) را از داخل وب‌سرورها خارج کنیم.

یکی از بهترین روش‌ها این است که اطلاعات Session در یک فضای ذخیره‌سازی دائمی مانند:

- پایگاه داده رابطه‌ای (Relational Database)
- پایگاه داده NoSQL

نگهداری شوند.

در این حالت، تمامی وب‌سرورهای موجود در کلاستر می‌توانند اطلاعات Session را از این فضای ذخیره‌سازی مشترک دریافت کنند.

به چنین معماری **Stateless Web Tier** گفته می‌شود.

---
###### 📄 صفحه 19

# Stateful Architecture

> A stateful server and stateless server has some key differences. A stateful server remembers client data (state) from one request to the next. A stateless server keeps no state information. Figure 1-12 shows an example of a stateful architecture.

بین **Stateful Server** و **Stateless Server** تفاوت‌های اساسی وجود دارد.

در یک **Stateful Server**، اطلاعات مربوط به کاربر (State) بین درخواست‌های مختلف نگهداری می‌شود؛ یعنی سرور وضعیت قبلی کاربر را به خاطر می‌سپارد.

در مقابل، **Stateless Server** هیچ اطلاعاتی از وضعیت قبلی کاربران ذخیره نمی‌کند و هر درخواست را کاملاً مستقل پردازش می‌کند.

---

![Stateful Architecture](design-system/images/System-Design-Interview-page19-image1.jpg)

---

> Figure 1-12 shows an example of a stateful architecture.

شکل ۱-۱۲ نمونه‌ای از یک معماری **Stateful** را نمایش می‌دهد.

---

> In Figure 1-12, user A’s session data and profile image are stored in Server 1. To authenticate User A, HTTP requests must be routed to Server 1. If a request is sent to other servers like Server 2, authentication would fail because Server 2 does not contain User A’s session data.
>
> Similarly, all HTTP requests from User B must be routed to Server 2; all requests from User C must be sent to Server 3.
>
> The issue is that every request from the same client must be routed to the same server. This can be done with sticky sessions in most load balancers [10]; however, this adds the overhead. Adding or removing servers is much more difficult with this approach. It is also challenging to handle server failures.


در شکل ۱-۱۲، اطلاعات Session و تصویر پروفایل **User A** روی **Server 1** ذخیره شده‌اند.

بنابراین، برای احراز هویت User A، تمامی درخواست‌های HTTP او باید به **Server 1** ارسال شوند.

اگر درخواست به **Server 2** ارسال شود، عملیات احراز هویت شکست می‌خورد؛ زیرا اطلاعات Session کاربر در آن سرور وجود ندارد.

به همین ترتیب:

- تمامی درخواست‌های User B باید به Server 2 ارسال شوند.
- تمامی درخواست‌های User C باید به Server 3 ارسال شوند.

مشکل اصلی این معماری این است که تمام درخواست‌های یک کاربر باید همیشه به همان سرور قبلی هدایت شوند.

این کار معمولاً با استفاده از **Sticky Session** در Load Balancer انجام می‌شود، اما این روش معایبی دارد:

- سربار (Overhead) بیشتری ایجاد می‌کند.
- اضافه یا حذف کردن سرورها دشوارتر می‌شود.
- مدیریت خرابی سرورها پیچیده‌تر خواهد بود.

---
###### 📄 صفحه 20

# Stateless Architecture

> Figure 1-13 shows the stateless architecture.


شکل ۱-۱۳ معماری **Stateless** را نمایش می‌دهد.

---

![Stateless Architecture](design-system/images/System-Design-Interview-page20-image1.jpg)

---

> In this stateless architecture, HTTP requests from users can be sent to any web servers, which fetch state data from a shared data store. State data is stored in a shared data store and kept out of web servers. A stateless system is simpler, more robust, and scalable.


در معماری **Stateless**، درخواست‌های HTTP کاربران می‌توانند به هر وب‌سروری ارسال شوند.

وب‌سرور در صورت نیاز اطلاعات Session یا سایر داده‌های مربوط به وضعیت کاربر را از یک **Shared Data Store** دریافت می‌کند.

بنابراین:

- اطلاعات State داخل وب‌سرورها نگهداری نمی‌شود.
- همه سرورها از یک منبع داده مشترک استفاده می‌کنند.

مزایای این معماری عبارت‌اند از:

- سادگی بیشتر
- مقاومت بالاتر در برابر خرابی
- مقیاس‌پذیری بسیار بهتر

---

> Figure 1-14 shows the updated design with a stateless web tier.

شکل ۱-۱۴ نسخه به‌روزشده معماری را با استفاده از **Stateless Web Tier** نمایش می‌دهد.

---

![Stateless Web Tier](design-system/images/System-Design-Interview-page20-image2.jpg)

---

> In Figure 1-14, we move the session data out of the web tier and store them in the persistent data store. The shared data store could be a relational database, Memcached/Redis, NoSQL, etc. The NoSQL data store is chosen as it is easy to scale. Autoscaling means adding or removing web servers automatically based on the traffic load. After the state data is removed out of web servers, auto-scaling of the web tier is easily achieved by adding or removing servers based on traffic load.
>
> Your website grows rapidly and attracts a significant number of users internationally. To improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial.


در شکل ۱-۱۴ اطلاعات Session از وب‌سرورها خارج شده و در یک فضای ذخیره‌سازی دائمی قرار گرفته‌اند.

این فضای ذخیره‌سازی مشترک می‌تواند یکی از گزینه‌های زیر باشد:

- Relational Database
- Redis
- Memcached
- NoSQL Database

در این مثال، **NoSQL** انتخاب شده است؛ زیرا توسعه و مقیاس‌پذیری آن ساده‌تر است.

مفهوم **Auto Scaling** به این معناست که سیستم بر اساس میزان ترافیک، به‌صورت خودکار وب‌سرورها را اضافه یا حذف می‌کند.

از آنجا که اطلاعات Session دیگر داخل وب‌سرورها ذخیره نمی‌شوند، اضافه یا حذف کردن سرورها بدون نگرانی از دست رفتن Session کاربران امکان‌پذیر خواهد بود.

در ادامه، با رشد سریع وب‌سایت و افزایش کاربران از نقاط مختلف جهان، برای افزایش **Availability** و بهبود **User Experience** در مناطق جغرافیایی مختلف، استفاده از **Multiple Data Centers** ضروری خواهد بود.

---


###### 📄 صفحه 21

# Data Centers

> Figure 1-15 shows an example setup with two data centers. In normal operation, users are geoDNS-routed, also known as geo-routed, to the closest data center, with a split traffic of x% in US-East and (100 – x)% in US-West. geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.


شکل ۱-۱۵ نمونه‌ای از معماری شامل **دو مرکز داده (Data Center)** را نشان می‌دهد.

در حالت عادی، کاربران با استفاده از **GeoDNS** (که با نام **Geo Routing** نیز شناخته می‌شود) به نزدیک‌ترین مرکز داده هدایت می‌شوند.

فرض کنید درصدی از کاربران (**x%**) به مرکز داده **US-East** و باقی کاربران (**100−x%**) به مرکز داده **US-West** هدایت شوند.

**GeoDNS** نوعی سرویس DNS است که آدرس دامنه را بر اساس موقعیت جغرافیایی کاربر به مناسب‌ترین آدرس IP تبدیل می‌کند.

---

![Two Data Centers](design-system/images/System-Design-Interview-page21-image1.jpg)

---

> Figure 1-15 shows an example setup with two data centers.

شکل ۱-۱۵ نمونه‌ای از استقرار سیستم با دو مرکز داده را نمایش می‌دهد.

---

> In the event of any significant data center outage, we direct all traffic to a healthy data center. In Figure 1-16, data center 2 (US-West) is offline, and 100% of the traffic is routed to data center 1 (US-East).


در صورت بروز اختلال جدی در یکی از مراکز داده، تمام ترافیک به نزدیک‌ترین **مرکز داده سالم** هدایت می‌شود.

در شکل ۱-۱۶، مرکز داده شماره ۲ (**US-West**) از دسترس خارج شده است؛ بنابراین **۱۰۰٪ ترافیک** به مرکز داده شماره ۱ (**US-East**) منتقل می‌شود.

---

![Data Center Failover](design-system/images/System-Design-Interview-page21-image2.jpg)

---

# Challenges of Multi-Data Center Architecture

> Several technical challenges must be resolved to achieve multi-data center setup:


برای پیاده‌سازی معماری **چند مرکز داده (Multi-Data Center)** باید چند چالش مهم برطرف شود.

---

> • Traffic redirection: Effective tools are needed to direct traffic to the correct data center. GeoDNS can be used to direct traffic to the nearest data center depending on where a user is located.


### ۱. هدایت ترافیک (Traffic Redirection)

برای ارسال کاربران به مناسب‌ترین مرکز داده، به ابزارهایی نیاز است که بتوانند درخواست‌ها را به مقصد صحیح هدایت کنند.

یکی از رایج‌ترین راهکارها **GeoDNS** است که با توجه به موقعیت جغرافیایی کاربر، نزدیک‌ترین Data Center را انتخاب می‌کند.

---

> • Data synchronization: Users from different regions could use different local databases or caches. In failover cases, traffic might be routed to a data center where data is unavailable. A common strategy is to replicate data across multiple data centers. A previous study shows how Netflix implements asynchronous multi-data center replication [11].


### ۲. همگام‌سازی داده‌ها (Data Synchronization)

کاربران مناطق مختلف ممکن است به پایگاه داده یا کش محلی متفاوتی متصل باشند.

در شرایط **Failover**، ممکن است کاربر به مرکز داده‌ای هدایت شود که اطلاعات مورد نیاز او هنوز در آن وجود ندارد.

برای حل این مشکل معمولاً داده‌ها بین مراکز داده مختلف **Replication** می‌شوند.

یکی از نمونه‌های معروف، معماری **Netflix** است که از **Asynchronous Multi-Data Center Replication** استفاده می‌کند.

---

> • Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers [11].


### ۳. تست و استقرار (Test & Deployment)

در معماری چند مرکز داده، باید وب‌سایت یا اپلیکیشن از نقاط جغرافیایی مختلف مورد آزمایش قرار گیرد.

همچنین استفاده از ابزارهای **استقرار خودکار (Automated Deployment)** اهمیت زیادی دارد تا تمامی مراکز داده نسخه‌ای یکسان از سرویس را اجرا کنند.

---

> To further scale our system, we need to decouple different components of the system so they can be scaled independently. Messaging queue is a key strategy employed by many real-world distributed systems to solve this problem.


برای اینکه سیستم را بیش از این مقیاس‌پذیر کنیم، لازم است اجزای مختلف آن را از یکدیگر **Decouple** کنیم تا هر بخش بتواند به‌صورت مستقل مقیاس‌پذیر باشد.

یکی از مهم‌ترین راهکارهایی که در سیستم‌های توزیع‌شده واقعی برای رسیدن به این هدف استفاده می‌شود، **Message Queue** است.

---
###### 📄 صفحه 22

# Message Queue

> A message queue is a durable component, stored in memory, that supports asynchronous communication. It serves as a buffer and distributes asynchronous requests. The basic architecture of a message queue is simple. Input services, called producers/publishers, create messages, and publish them to a message queue. Other services or servers, called consumers/subscribers, connect to the queue, and perform actions defined by the messages. The model is shown in Figure 1-17.


**Message Queue** یک مؤلفه پایدار برای برقراری ارتباط **Asynchronous** بین سرویس‌ها است.

این مؤلفه مانند یک **Buffer** عمل می‌کند و درخواست‌ها را به صورت غیرهمزمان بین سرویس‌های مختلف توزیع می‌کند.

معماری Message Queue بسیار ساده است.

در این معماری:

- سرویس‌هایی که پیام تولید می‌کنند **Producer** یا **Publisher** نام دارند.
- این سرویس‌ها پیام‌های خود را داخل Message Queue قرار می‌دهند.
- سرویس‌های دیگر که **Consumer** یا **Subscriber** نام دارند، پیام‌ها را از صف دریافت کرده و عملیات مربوط به آن‌ها را اجرا می‌کنند.

---

![Message Queue Architecture](design-system/images/System-Design-Interview-page22-image1.jpg)

---

> Figure 1-17 shows the basic architecture of a message queue.

شکل ۱-۱۷ معماری پایه یک **Message Queue** را نمایش می‌دهد.

---

> Decoupling makes the message queue a preferred architecture for building a scalable and reliable application. With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.


جدا کردن وابستگی بین سرویس‌ها (**Decoupling**) باعث شده است که **Message Queue** یکی از محبوب‌ترین معماری‌ها برای ساخت سیستم‌های **Scalable** و **Reliable** باشد.

در این معماری:

- اگر **Consumer** در دسترس نباشد، **Producer** همچنان می‌تواند پیام خود را داخل صف قرار دهد.
- اگر **Producer** از دسترس خارج شود، **Consumer** همچنان می‌تواند پیام‌های موجود در صف را پردازش کند.

به همین دلیل، وابستگی مستقیم بین سرویس‌ها از بین می‌رود و تحمل خطا (Fault Tolerance) سیستم افزایش می‌یابد.

---

> Consider the following use case: your application supports photo customization, including cropping, sharpening, blurring, etc. Those customization tasks take time to complete. In Figure 1-18, web servers publish photo processing jobs to the message queue. Photo processing workers pick up jobs from the message queue and asynchronously perform photo customization tasks. The producer and the consumer can be scaled independently. When the size of the queue becomes large, more workers are added to reduce the processing time. However, if the queue is empty most of the time, the number of workers can be reduced.


فرض کنید اپلیکیشن شما امکان ویرایش تصاویر را فراهم می‌کند؛ مانند:

- Crop
- Sharpen
- Blur
- و سایر پردازش‌های تصویری

این عملیات معمولاً زمان‌بر هستند و مناسب نیست کاربران تا پایان پردازش منتظر بمانند.

در شکل ۱-۱۸:

- وب‌سرورها درخواست‌های پردازش تصویر را داخل **Message Queue** قرار می‌دهند.
- Workerها این درخواست‌ها را از صف دریافت می‌کنند.
- پردازش تصویر به‌صورت **Asynchronous** انجام می‌شود.

مزیت مهم این معماری این است که **Producer** و **Consumer** می‌توانند کاملاً مستقل از یکدیگر مقیاس‌پذیر باشند.

اگر تعداد پیام‌های موجود در صف زیاد شود، می‌توان Workerهای بیشتری اضافه کرد تا سرعت پردازش افزایش پیدا کند.

در مقابل، اگر صف تقریباً همیشه خالی باشد، تعداد Workerها کاهش پیدا می‌کند تا منابع سیستم هدر نرود.

---

![Photo Processing with Message Queue](design-system/images/System-Design-Interview-page22-image2.jpg)

