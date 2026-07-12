## متن کتاب

> **CHAPTER 1:** Designing a system that supports millions of users is challenging, and it is a journey that requires continuous refinement and endless improvement. In this chapter, we build a system that supports a single user and gradually scale it up to serve millions of users. After reading this chapter, you will master a handful of techniques that will help you to crack the system design interview questions.

---

# ترجمه

**فصل ۱:** طراحی سیستمی که بتواند از **میلیون‌ها کاربر** پشتیبانی کند، کاری پیچیده و چالش‌برانگیز است. این فرایند یک مسیر تدریجی است که به **بهبود مستمر (Continuous Refinement)** و **تکامل بی‌پایان (Endless Improvement)** نیاز دارد.

در این فصل، ابتدا سیستمی را طراحی می‌کنیم که تنها از **یک کاربر** پشتیبانی می‌کند و سپس قدم‌به‌قدم آن را گسترش می‌دهیم تا بتواند به **میلیون‌ها کاربر** سرویس ارائه دهد.

پس از مطالعه‌ی این فصل، با مجموعه‌ای از تکنیک‌ها و الگوهای مهم در طراحی سیستم آشنا خواهید شد که در حل سؤالات مصاحبه‌ی **System Design** به شما کمک می‌کنند.

---

## متن کتاب

> **Single server setup:** A journey of a thousand miles begins with a single step, and building a complex system is no different. To start with something simple, everything is running on a single server. Figure 1-1 shows the illustration of a single server setup where everything is running on one server: web app, database, cache, etc.

---

# ترجمه

**راه‌اندازی تک‌سروری:** راه هزار مایلی با یک قدم آغاز می‌شود، و ساخت یک سیستم پیچیده نیز تفاوتی ندارد. برای شروع، ابتدا از چیزی ساده آغاز می‌کنیم: همه چیز روی یک سرور واحد اجرا می‌شود. شکل ۱-۱ نمایی از یک راه‌اندازی تک‌سروری را نشان می‌دهد که در آن همه چیز — از جمله اپلیکیشن وب، پایگاه داده، کش و غیره — روی یک سرور اجرا می‌شود.

![Single server setup](design-system/images/System-Design-Interview-page6-image1.jpg)

## متن کتاب

> **Single server setup:** To understand this setup, it is helpful to investigate the request flow and traffic source. Let us first look at the request flow (Figure 1-2).

---

# ترجمه

**راه‌اندازی تک‌سروری:** برای درک بهتر این ساختار، بررسی جریان درخواست‌ها (request flow) و منبع ترافیک مفید خواهد بود. ابتدا نگاهی به جریان درخواست‌ها می‌اندازیم (شکل ۱-۲).

![Figure 1-2 – Request flow](design-system/images/System-Design-Interview-page6-image2.jpg)

## متن کتاب

>1. Users access websites through domain names, such as api.mysite.com. Usually, the
Domain Name System (DNS) is a paid service provided by 3rd parties and not hosted by
our servers.
2. Internet Protocol (IP) address is returned to the browser or mobile app. In the example,
IP address 15.125.23.214 is returned.
3. Once the IP address is obtained, Hypertext Transfer Protocol (HTTP) [1] requests are
sent directly to your web server.
4. The web server returns HTML pages or JSON response for rendering.
Next, let us examine the traffic source. The traffic to your web server comes from two
sources: web application and mobile application.
• Web application: it uses a combination of server-side languages (Java, Python, etc.) to
handle business logic, storage, etc., and client-side languages (HTML and JavaScript) for
presentation.
• Mobile application: HTTP protocol is the communication protocol between the mobile
app and the web server. JavaScript Object Notation (JSON) is commonly used API
response format to transfer data due to its simplicity. An example of the API response in
JSON format is shown below:
GET/users/12 - Retrieve user object for id = 12

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

1

}

---

# ترجمه

۱. کاربران از طریق نام دامنه (domain name)، مانند api.mysite.com، به وب‌سایت‌ها دسترسی پیدا می‌کنند. معمولاً سیستم نام دامنه (DNS) یک سرویس پولی است که توسط شرکت‌های شخص ثالث ارائه می‌شود و روی سرورهای خودمان میزبانی نمی‌شود.

۲. آدرس IP (Internet Protocol) به مرورگر یا اپلیکیشن موبایل بازگردانده می‌شود. در این مثال، آدرس IP برابر با 15.125.23.214 بازگردانده شده است.

۳. پس از دریافت آدرس IP، درخواست‌های HTTP مستقیماً به سرور وب شما ارسال می‌شوند.

۴. سرور وب صفحات HTML یا پاسخ JSON را برای رندر شدن بازمی‌گرداند.

در ادامه، به بررسی منبع ترافیک می‌پردازیم. ترافیک ورودی به سرور وب شما از دو منبع می‌آید: اپلیکیشن وب و اپلیکیشن موبایل.

• **اپلیکیشن وب:** ترکیبی از زبان‌های سمت سرور (مانند Java، Python و غیره) برای مدیریت منطق تجاری (business logic)، ذخیره‌سازی و غیره، و زبان‌های سمت کلاینت (HTML و JavaScript) برای نمایش (presentation) استفاده می‌کند.

• **اپلیکیشن موبایل:** پروتکل HTTP، پروتکل ارتباطی بین اپلیکیشن موبایل و سرور وب است. فرمت JSON (JavaScript Object Notation) به دلیل سادگی‌اش، متداول‌ترین فرمت پاسخ API برای انتقال داده است. نمونه‌ای از پاسخ API با فرمت JSON در زیر نشان داده شده است:

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

## متن کتاب

> **Database:** With the growth of the user base, one server is not enough, and we need multiple servers: one
for web/mobile traffic, the other for the database (Figure 1-3). Separating web/mobile traffic
(web tier) and database (data tier) servers allows them to be scaled independently.

---

# ترجمه

**پایگاه داده:** با رشد پایگاه کاربران، یک سرور دیگر کافی نیست و به چند سرور نیاز داریم: یکی برای ترافیک وب/موبایل و دیگری برای پایگاه داده (شکل ۱-۳). جدا کردن سرورهای ترافیک وب/موبایل (لایه‌ی وب یا web tier) از سرور پایگاه داده (لایه‌ی داده یا data tier) این امکان را فراهم می‌کند که هر کدام به‌طور مستقل مقیاس‌پذیر (scale) شوند.

![Figure 1-3](design-system/images/System-Design-Interview-page7-image1.jpg)

## متن کتاب

> **Which databases to use?** You can choose between a traditional relational database and a non-relational database. Let us examine their differences.
>
> Relational databases are also called a relational database management system (RDBMS) or SQL database. The most popular ones are MySQL, Oracle database, PostgreSQL, etc. Relational databases represent and store data in tables and rows. You can perform join operations using SQL across different database tables.
>
> Non-Relational databases are also called NoSQL databases. Popular ones are CouchDB, Neo4j, Cassandra, HBase, Amazon DynamoDB, etc. [2]. These databases are grouped into four categories: key-value stores, graph stores, column stores, and document stores. Join operations are generally not supported in non-relational databases.
>
> For most developers, relational databases are the best option because they have been around for over 40 years and historically, they have worked well. However, if relational databases are not suitable for your specific use cases, it is critical to explore beyond relational databases. Non-relational databases might be the right choice if:
> • Your application requires super-low latency.
> • Your data are unstructured, or you do not have any relational data.
> • You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
> • You need to store a massive amount of data.

---

# ترجمه

**کدام پایگاه‌های داده را استفاده کنیم؟** شما می‌توانید بین یک پایگاه داده‌ی رابطه‌ای سنتی (relational) و یک پایگاه داده‌ی غیررابطه‌ای (non-relational) انتخاب کنید. بیایید تفاوت‌های آن‌ها را بررسی کنیم.

پایگاه‌های داده‌ی رابطه‌ای را سیستم مدیریت پایگاه داده‌ی رابطه‌ای (RDBMS) یا پایگاه داده‌ی SQL نیز می‌نامند. محبوب‌ترین آن‌ها MySQL، Oracle Database، PostgreSQL و غیره هستند. پایگاه‌های داده‌ی رابطه‌ای، داده‌ها را به‌صورت جدول و سطر (table و row) نمایش می‌دهند و ذخیره می‌کنند. شما می‌توانید با استفاده از SQL، عملیات join را بین جداول مختلف پایگاه داده انجام دهید.

پایگاه‌های داده‌ی غیررابطه‌ای را پایگاه داده‌ی NoSQL نیز می‌نامند. محبوب‌ترین آن‌ها CouchDB، Neo4j، Cassandra، HBase، Amazon DynamoDB و غیره هستند [۲]. این پایگاه‌های داده در چهار دسته قرار می‌گیرند: فروشگاه‌های کلید-مقدار (key-value store)، فروشگاه‌های گراف (graph store)، فروشگاه‌های ستونی (column store) و فروشگاه‌های سندی (document store). عملیات join معمولاً در پایگاه‌های داده‌ی غیررابطه‌ای پشتیبانی نمی‌شود.

برای اکثر توسعه‌دهندگان، پایگاه‌های داده‌ی رابطه‌ای بهترین گزینه هستند، زیرا بیش از ۴۰ سال است که وجود دارند و از نظر تاریخی عملکرد خوبی داشته‌اند. اما اگر پایگاه‌های داده‌ی رابطه‌ای برای موارد استفاده‌ی خاص شما مناسب نیستند، بررسی گزینه‌های فراتر از پایگاه‌های داده‌ی رابطه‌ای ضروری است. پایگاه‌های داده‌ی غیررابطه‌ای ممکن است در موارد زیر انتخاب مناسبی باشند:

• اپلیکیشن شما به تأخیر (latency) بسیار پایینی نیاز دارد.
• داده‌های شما ساختارنیافته (unstructured) هستند یا هیچ داده‌ی رابطه‌ای ندارید.
• فقط نیاز به سریالایز و دیسریالایز کردن داده (JSON، XML، YAML و غیره) دارید.
• نیاز به ذخیره‌ی حجم عظیمی از داده دارید.

## متن کتاب

> **Vertical scaling vs horizontal scaling:** Vertical scaling, referred to as "scale up", means the process of adding more power (CPU, RAM, etc.) to your servers. Horizontal scaling, referred to as "scale-out", allows you to scale by adding more servers into your pool of resources.
>
> When traffic is low, vertical scaling is a great option, and the simplicity of vertical scaling is its main advantage. Unfortunately, it comes with serious limitations.
> • Vertical scaling has a hard limit. It is impossible to add unlimited CPU and memory to a single server.
> • Vertical scaling does not have failover and redundancy. If one server goes down, the website/app goes down with it completely.
>
> Horizontal scaling is more desirable for large scale applications due to the limitations of vertical scaling.
>
> In the previous design, users are connected to the web server directly. Users will unable to access the website if the web server is offline. In another scenario, if many users access the web server simultaneously and it reaches the web server's load limit, users generally experience slower response or fail to connect to the server. A load balancer is the best technique to address these problems.

---

# ترجمه

**مقیاس‌پذیری عمودی در برابر مقیاس‌پذیری افقی:** مقیاس‌پذیری عمودی (vertical scaling)، که به آن «scale up» نیز گفته می‌شود، به معنای افزودن قدرت بیشتر (CPU، RAM و غیره) به سرورهای شماست. مقیاس‌پذیری افقی (horizontal scaling)، که به آن «scale-out» نیز گفته می‌شود، به شما امکان می‌دهد با افزودن سرورهای بیشتر به مجموعه‌ی منابع خود، مقیاس‌پذیری را افزایش دهید.

هنگامی که ترافیک کم است، مقیاس‌پذیری عمودی گزینه‌ی بسیار خوبی است و سادگی آن مزیت اصلی‌اش محسوب می‌شود. اما متأسفانه این روش با محدودیت‌های جدی همراه است:

• مقیاس‌پذیری عمودی یک محدودیت سخت‌افزاری دارد. افزودن CPU و حافظه‌ی نامحدود به یک سرور واحد غیرممکن است.
• مقیاس‌پذیری عمودی فاقد قابلیت failover و افزونگی (redundancy) است. اگر یک سرور از کار بیفتد، کل وب‌سایت/اپلیکیشن به‌طور کامل از دسترس خارج می‌شود.

به دلیل محدودیت‌های مقیاس‌پذیری عمودی، مقیاس‌پذیری افقی برای اپلیکیشن‌های بزرگ‌مقیاس مطلوب‌تر است.

در طراحی قبلی، کاربران مستقیماً به سرور وب متصل می‌شدند. اگر سرور وب آفلاین شود، کاربران قادر به دسترسی به وب‌سایت نخواهند بود. در سناریویی دیگر، اگر تعداد زیادی از کاربران به‌طور همزمان به سرور وب دسترسی پیدا کنند و از حد بار (load limit) سرور فراتر بروند، کاربران معمولاً پاسخ کندتری دریافت می‌کنند یا اصلاً نمی‌توانند به سرور متصل شوند. یک بالانسر بار (load balancer) بهترین راهکار برای رفع این مشکلات است.