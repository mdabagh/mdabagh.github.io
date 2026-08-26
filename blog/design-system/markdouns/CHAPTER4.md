> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۵۱

> **CHAPTER 4: DESIGN A RATE LIMITER**
> In a network system, a rate limiter is used to control the rate of traffic sent by a client or a service. In the HTTP world, a rate limiter limits the number of client requests allowed to be sent over a specified period. If the API request count exceeds the threshold defined by the rate limiter, all the excess calls are blocked. Here are a few examples:
> • A user can write no more than 2 posts per second.
> • You can create a maximum of 10 accounts per day from the same IP address.
> • You can claim rewards no more than 5 times per week from the same device.
>
> In this chapter, you are asked to design a rate limiter. Before starting the design, we first look at the benefits of using an API rate limiter:
> • Prevent resource starvation caused by Denial of Service (DoS) attack [1]. Almost all APIs published by large tech companies enforce some form of rate limiting. For example, Twitter limits the number of tweets to 300 per 3 hours [2]. Google docs APIs have the following default limit: 300 per user per 60 seconds for read requests [3]. A rate limiter prevents DoS attacks, either intentional or unintentional, by blocking the excess calls.
> • Reduce cost. Limiting excess requests means fewer servers and allocating more resources to high priority APIs.
> • Prevent servers from being overloaded.

**فصل ۴: طراحی یک محدودکننده نرخ (Rate Limiter)**

در یک سیستم شبکه‌ای، از **محدودکننده نرخ (Rate Limiter)** برای کنترل نرخ ترافیک ارسال‌شده توسط یک کلاینت یا سرویس استفاده می‌شود. در دنیای HTTP، Rate Limiter تعداد درخواست‌های کلاینت را در یک بازه زمانی مشخص محدود می‌کند. اگر تعداد درخواست‌های API از آستانه تعریف‌شده تجاوز کند، تمام فراخوانی‌های اضافی **مسدود (Blocked)** می‌شوند.

چند مثال:
- یک کاربر نمی‌تواند بیش از ۲ پست در ثانیه ارسال کند.
- حداکثر ۱۰ حساب کاربری در روز از یک آدرس IP می‌توان ایجاد کرد.
- حداکثر ۵ بار در هفته از یک دستگاه می‌توان پاداش دریافت کرد.

**مزایای استفاده از Rate Limiter:**
- **جلوگیری از حملات DoS (Denial of Service):** تقریباً تمام APIهای شرکت‌های بزرگ فناوری نوعی محدودیت نرخ اعمال می‌کنند. برای مثال، توییتر تعداد تویت‌ها را به ۳۰۰ در ۳ ساعت محدود می‌کند [۲].
- **کاهش هزینه:** محدود کردن درخواست‌های اضافی به معنای سرورهای کمتر و تخصیص منابع بیشتر به APIهای با اولویت بالا است.
- **جلوگیری از بیش‌باری (Overload) سرورها.**

---

###### 📄 صفحه ۵۲

> **Step 1 - Understand the problem and establish design scope**
>
> Candidate: What kind of rate limiter are we going to design? Is it a client-side rate limiter or server-side API rate limiter?
> Interviewer: Great question. We focus on the server-side API rate limiter.
> Candidate: Does the rate limiter throttle API requests based on IP, the user ID, or other properties?
> Interviewer: The rate limiter should be flexible enough to support different sets of throttle rules.
> Candidate: What is the scale of the system? Is it built for a startup or a big company with a large user base?
> Interviewer: The system must be able to handle a large number of requests.
> Candidate: Will the system work in a distributed environment?
> Interviewer: Yes.
> Candidate: Is the rate limiter a separate service or should it be implemented in application code?
> Interviewer: It is a design decision up to you.
> Candidate: Do we need to inform users who are throttled?
> Interviewer: Yes.
>
> **Requirements:**
> • Accurately limit excessive requests.
> • Low latency. The rate limiter should not slow down HTTP response time.
> • Use as little memory as possible.
> • Distributed rate limiting.
> • Exception handling. Show clear exceptions to users when their requests are throttled.
> • High fault tolerance.

### مرحله ۱ - درک مسئله و تعیین محدوده طراحی

**کاندیدا:** چه نوع Rate Limiterی قرار است طراحی کنیم؟ سمت کلاینت است یا سمت سرور (Server-side API Rate Limiter)؟
**مصاحبه‌گر:** سؤال خوبی است. روی Rate Limiter سمت سرور تمرکز می‌کنیم.
**کاندیدا:** آیا Rate Limiter درخواست‌ها را بر اساس IP، شناسه کاربر یا سایر ویژگی‌ها محدود می‌کند؟
**مصاحبه‌گر:** Rate Limiter باید به اندازه کافی انعطاف‌پذیر باشد تا مجموعه‌های مختلفی از قوانین محدودیت را پشتیبانی کند.
**کاندیدا:** مقیاس سیستم چقدر است؟ برای یک استارتاپ ساخته می‌شود یا شرکت بزرگ با تعداد کاربر زیاد؟
**مصاحبه‌گر:** سیستم باید بتواند تعداد زیادی درخواست را مدیریت کند.
**کاندیدا:** آیا سیستم در محیط توزیع‌شده کار می‌کند؟
**مصاحبه‌گر:** بله.
**کاندیدا:** آیا Rate Limiter یک سرویس جداگانه است یا باید در کد اپلیکیشن پیاده‌سازی شود؟
**مصاحبه‌گر:** این یک تصمیم طراحی است که به شما بستگی دارد.
**کاندیدا:** آیا باید به کاربرانی که محدود شده‌اند اطلاع دهیم؟
**مصاحبه‌گر:** بله.

**نیازمندی‌ها:**
- محدود کردن دقیق درخواست‌های اضافی
- **Latency پایین:** Rate Limiter نباید زمان پاسخ HTTP را کاهش دهد
- استفاده از حداقل حافظه ممکن
- **محدودیت نرخ توزیع‌شده (Distributed Rate Limiting)**
- **مدیریت استثنا:** نمایش استثنای واضح به کاربران هنگام محدود شدن درخواست‌ها
- **تحمل خطای بالا (High Fault Tolerance)**

---

###### 📄 صفحه ۵۳

> **Step 2 - Propose high-level design and get buy-in**
>
> **Where to put the rate limiter?**
> • Client-side implementation. Generally speaking, client is an unreliable place to enforce rate limiting because client requests can easily be forged by malicious actors.
> • Server-side implementation. Figure 4-1 shows a rate limiter that is placed on the server-side.
> • Rate limiter middleware. Instead of putting a rate limiter at the API servers, we create a rate limiter middleware, which throttles requests to your APIs as shown in Figure 4-2.
>
> Let us use an example in Figure 4-3 to illustrate how rate limiting works in this design. Assume our API allows 2 requests per second, and a client sends 3 requests to the server within a second. The first two requests are routed to API servers. However, the rate limiter middleware throttles the third request and returns a HTTP status code 429. The HTTP 429 response status code indicates a user has sent too many requests.

### مرحله ۲ - ارائه طراحی سطح بالا و جلب تأیید

**Rate Limiter کجا قرار بگیرد؟**

- **پیاده‌سازی سمت کلاینت:** به‌طور کلی، کلاینت مکانی غیرقابل اعتماد برای اعمال محدودیت نرخ است، زیرا درخواست‌های کلاینت به‌راحتی توسط بازیگران مخرب جعل می‌شوند.
- **پیاده‌سازی سمت سرور:** شکل ۴-۱ Rate Limiterی را نشان می‌دهد که در سمت سرور قرار دارد.
- **میان‌افزار محدودکننده نرخ (Rate Limiter Middleware):** به جای قرار دادن Rate Limiter در سرورهای API، یک میان‌افزار Rate Limiter ایجاد می‌کنیم که درخواست‌ها را محدود می‌کند (شکل ۴-۲).

شکل ۴-۳ نحوه عملکرد Rate Limiting در این طراحی را نشان می‌دهد. فرض کنید API ما ۲ درخواست در ثانیه مجاز می‌داند و یک کلاینت ۳ درخواست در یک ثانیه ارسال می‌کند. دو درخواست اول به سرورهای API هدایت می‌شوند، اما میان‌افزار Rate Limiter درخواست سوم را محدود کرده و **کد وضعیت HTTP 429** را برمی‌گرداند. این کد وضعیت نشان‌دهنده این است که کاربر درخواست‌های بیش از حد ارسال کرده است.

![Figure 4-1](design-system/images/System-Design-Interview-page53-image1.jpg)

![Figure 4-2](design-system/images/System-Design-Interview-page53-image2.jpg)

![Figure 4-3](design-system/images/System-Design-Interview-page54-image1.jpg)

---

###### 📄 صفحه ۵۴

> Cloud microservices [4] have become widely popular and rate limiting is usually implemented within a component called API gateway. API gateway is a fully managed service that supports rate limiting, SSL termination, authentication, IP whitelisting, servicing static content, etc.
>
> While designing a rate limiter, an important question to ask ourselves is: where should the rate limiter be implemented, on the server-side or in a gateway? There is no absolute answer. It depends on your company's current technology stack, engineering resources, priorities, goals, etc. Here are a few general guidelines:
> • Evaluate your current technology stack, such as programming language, cache service, etc.
> • Identify the rate limiting algorithm that fits your business needs.
> • If you have already used microservice architecture and included an API gateway in the design, you may add a rate limiter to the API gateway.
> • Building your own rate limiting service takes time. If you do not have enough engineering resources, a commercial API gateway is a better option.

**میکروسرویس‌های ابری [۴]** به‌طور گسترده‌ای محبوب شده‌اند و محدودیت نرخ معمولاً در مؤلفه‌ای به نام **API Gateway** پیاده‌سازی می‌شود. API Gateway یک سرویس کاملاً مدیریت‌شده است که از Rate Limiting، پایان‌دادن SSL، احراز هویت، لیست سفید IP، ارائه محتوای استاتیک و غیره پشتیبانی می‌کند.

**دستورالعمل‌های کلی:**
- استک فناوری فعلی خود را ارزیابی کنید (زبان برنامه‌نویسی، سرویس کش و...).
- الگوریتم محدودیت نرخی را که با نیازهای کسب‌وکار شما سازگار است شناسایی کنید.
- اگر قبلاً از معماری میکروسرویس استفاده کرده‌اید و API Gateway در طراحی دارید، می‌توانید Rate Limiter را به API Gateway اضافه کنید.
- ساخت سرویس Rate Limiting اختصاصی زمان‌بر است. اگر منابع مهندسی کافی ندارید، یک API Gateway تجاری گزینه بهتری است.

---

###### 📄 صفحه ۵۴ (ادامه)

> **Algorithms for rate limiting:** Rate limiting can be implemented using different algorithms, and each of them has distinct pros and cons. Here is a list of popular algorithms:
> • Token bucket
> • Leaking bucket
> • Fixed window counter
> • Sliding window log
> • Sliding window counter

### الگوریتم‌های Rate Limiting

Rate Limiting را می‌توان با الگوریتم‌های مختلفی پیاده‌سازی کرد و هرکدام مزایا و معایب خاص خود را دارند. در ادامه الگوریتم‌های محبوب فهرست شده‌اند:

- Token Bucket (سطل توکن)
- Leaking Bucket (سطل نشتی)
- Fixed Window Counter (شمارنده پنجره ثابت)
- Sliding Window Log (گزارش پنجره لغزنده)
- Sliding Window Counter (شمارنده پنجره لغزنده)

---

###### 📄 صفحه ۵۵

> **Token bucket algorithm:** The token bucket algorithm is widely used for rate limiting. It is simple, well understood and commonly used by internet companies. Both Amazon [5] and Stripe [6] use this algorithm to throttle their API requests.
>
> The token bucket algorithm work as follows:
> • A token bucket is a container that has pre-defined capacity. Tokens are put in the bucket at preset rates periodically. Once the bucket is full, no more tokens are added. As shown in Figure 4-4, the token bucket capacity is 4. The refiller puts 2 tokens into the bucket every second. Once the bucket is full, extra tokens will overflow.
> • Each request consumes one token. When a request arrives, we check if there are enough tokens in the bucket. Figure 4-5 explains how it works.
> • If there are enough tokens, we take one token out for each request, and the request goes through.
> • If there are not enough tokens, the request is dropped.

### الگوریتم Token Bucket (سطل توکن)

الگوریتم Token Bucket به‌طور گسترده‌ای برای Rate Limiting استفاده می‌شود. این الگوریتم **ساده، خوب درک‌شده و رایج** است. هم **آمازون [۵]** و هم **Stripe [۶]** از این الگوریتم برای محدود کردن درخواست‌های API خود استفاده می‌کنند.

> ***یادداشت شخصی***
>
> 🔗 **ترجمه مقاله Stripe:** [ترجمه Rate Limiting در Stripe](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=StripeRateLimiters)
>
> این مقاله توضیح می‌دهد Stripe چگونه ۴ نوع مختلف Rate Limiting را در مقیاس واقعی پیاده‌سازی کرده است.

نحوه عملکرد:
- **Token Bucket** یک ظرف با ظرفیت از پیش تعریف‌شده است. توکن‌ها با نرخ تنظیم‌شده به‌طور دوره‌ای در سطل قرار می‌گیرند. وقتی سطل پر شد، توکن بیشتری اضافه نمی‌شود. شکل ۴-۴ نشان می‌دهد ظرفیت سطل ۴ توکن است و هر ثانیه ۲ توکن اضافه می‌شود.
- **هر درخواست یک توکن مصرف می‌کند.** وقتی درخواستی می‌رسد، بررسی می‌کنیم آیا توکن کافی در سطل وجود دارد (شکل ۴-۵).
- اگر توکن کافی باشد، یک توکن برداشته شده و درخواست انجام می‌شود.
- اگر توکن کافی نباشد، درخواست **رد (Dropped)** می‌شود.

![Figure 4-4](design-system/images/System-Design-Interview-page55-image1.jpg)

![Figure 4-5](design-system/images/System-Design-Interview-page56-image1.jpg)

---

###### 📄 صفحه ۵۷

> Figure 4-6 illustrates how token consumption, refill, and rate limiting logic work. In this example, the token bucket size is 4, and the refill rate is 4 per 1 minute.
>
> The token bucket algorithm takes two parameters:
> • Bucket size: the maximum number of tokens allowed in the bucket
> • Refill rate: number of tokens put into the bucket every second
>
> How many buckets do we need? This varies, and it depends on the rate-limiting rules. Here are a few examples.
> • It is usually necessary to have different buckets for different API endpoints.
> • If we need to throttle requests based on IP addresses, each IP address requires a bucket.
> • If the system allows a maximum of 10,000 requests per second, it makes sense to have a global bucket shared by all requests.
>
> Pros:
> • The algorithm is easy to implement.
> • Memory efficient.
> • Token bucket allows a burst of traffic for short periods.
>
> Cons:
> • Two parameters in the algorithm are bucket size and token refill rate. However, it might be challenging to tune them properly.

شکل ۴-۶ نحوه مصرف توکن، پر کردن مجدد و منطق Rate Limiting را نشان می‌دهد. در این مثال، اندازه سطل ۴ است و نرخ پرکردن مجدد ۴ توکن در دقیقه است.

**پارامترهای الگوریتم:**
- **اندازه سطل (Bucket Size):** حداکثر تعداد توکن‌های مجاز در سطل
- **نرخ پرکردن (Refill Rate):** تعداد توکن‌هایی که هر ثانیه در سطل قرار می‌گیرند

**چند سطل نیاز داریم؟** این بستگی به قوانین Rate Limiting دارد:
- معمولاً برای نقاط انتهایی API مختلف به سطل‌های مختلف نیاز است.
- اگر محدودیت بر اساس آدرس IP باشد، هر IP به یک سطل نیاز دارد.
- اگر سیستم حداکثر ۱۰,۰۰۰ درخواست در ثانیه مجاز بداند، داشتن یک سطل مشترک (Global Bucket) منطقی است.

**مزایا:**
- الگوریتم پیاده‌سازی آسانی دارد.
- از حافظه بهینه استفاده می‌کند.
- اجازه ترافیک ناگهانی (Burst) در بازه‌های کوتاه را می‌دهد.

**معایب:**
- دو پارامتر (اندازه سطل و نرخ پرکردن) ممکن است تنظیم دقیق آن‌ها چالش‌برانگیز باشد.

---

###### 📄 صفحه ۵۸

> **Leaking bucket algorithm:** The leaking bucket algorithm is similar to the token bucket except that requests are processed at a fixed rate. It is usually implemented with a first-in-first-out (FIFO) queue. The algorithm works as follows:
> • When a request arrives, the system checks if the queue is full. If it is not full, the request is added to the queue.
> • Otherwise, the request is dropped.
> • Requests are pulled from the queue and processed at regular intervals.
>
> Leaking bucket algorithm takes the following two parameters:
> • Bucket size: it is equal to the queue size. The queue holds the requests to be processed at a fixed rate.
> • Outflow rate: it defines how many requests can be processed at a fixed rate, usually in seconds.
>
> Shopify, an ecommerce company, uses leaky buckets for rate-limiting [7].
>
> Pros:
> • Memory efficient given the limited queue size.
> • Requests are processed at a fixed rate therefore it is suitable for use cases that a stable outflow rate is needed.
>
> Cons:
> • A burst of traffic fills up the queue with old requests, and if they are not processed in time, recent requests will be rate limited.

### الگوریتم Leaking Bucket (سطل نشتی)

الگوریتم Leaking Bucket مشابه Token Bucket است با این تفاوت که درخواست‌ها با **نرخ ثابت** پردازش می‌شوند. معمولاً با یک **صف اولین ورود، اولین خروج (FIFO)** پیاده‌سازی می‌شود.

نحوه عملکرد:
- وقتی درخواستی می‌رسد، سیستم بررسی می‌کند آیا صف پر است. اگر پر نباشد، درخواست به صف اضافه می‌شود.
- در غیر این صورت، درخواست رد می‌شود.
- درخواست‌ها از صف کشیده شده و در بازه‌های زمانی منظم پردازش می‌شوند.

**پارامترها:**
- **اندازه سطل:** برابر با اندازه صف است. صف درخواست‌هایی را که با نرخ ثابت پردازش می‌شوند نگه می‌دارد.
- **نرخ خروج (Outflow Rate):** تعداد درخواست‌هایی که با نرخ ثابت پردازش می‌شوند (معمولاً بر حسب ثانیه).

شرکت **Shopify** از Leaking Bucket برای Rate Limiting استفاده می‌کند [۷].

> ***یادداشت شخصی***
>
> 🔗 **راهنما:** [مستندات Shopify - Rate Limits](https://help.shopify.com/en/api/reference/rest-admin-api-rate-limits)
>
> Shopify در مستندات رسمی خود توضیح می‌دهد چگونه API Rate Limiting را مدیریت می‌کند. از الگوریتم Leaking Bucket برای محدود کردن درخواست‌ها استفاده می‌شود.

**مزایا:** بهینه از حافظه استفاده می‌کند و پردازش درخواست‌ها با نرخ ثابت انجام می‌شود.
**معایب:** ترافیک ناگهانی صف را با درخواست‌های قدیمی پر می‌کند و درخواست‌های اخیر ممکن است محدود شوند.

![Figure 4-7](design-system/images/System-Design-Interview-page57-image1.jpg)

---

###### 📄 صفحه ۵۸ (ادامه)

> **Fixed window counter algorithm:** Fixed window counter algorithm works as follows:
> • The algorithm divides the timeline into fix-sized time windows and assign a counter for each window.
> • Each request increments the counter by one.
> • Once the counter reaches the pre-defined threshold, new requests are dropped until a new time window starts.
>
> Let us use a concrete example to see how it works. In Figure 4-8, the time unit is 1 second and the system allows a maximum of 3 requests per second. In each second window, if more than 3 requests are received, extra requests are dropped.
>
> A major problem with this algorithm is that a burst of traffic at the edges of time windows could cause more requests than allowed quota to go through.

### الگوریتم Fixed Window Counter (شمارنده پنجره ثابت)

نحوه عملکرد:
- الگوریتم خط زمانی را به پنجره‌های زمانی با **اندازه ثابت** تقسیم می‌کند و برای هر پنجره یک شمارنده اختصاص می‌دهد.
- هر درخواست شمارنده را یک واحد افزایش می‌دهد.
- وقتی شمارنده به آستانه از پیش تعریف‌شده رسید، درخواست‌های جدید تا شروع پنجره زمانی بعدی رد می‌شوند.

شکل ۴-۸ نمونه‌ای را نشان می‌دهد: واحد زمان ۱ ثانیه و سیستم حداکثر ۳ درخواست در ثانیه مجاز می‌داند. در هر پنجره ثانیه‌ای، اگر بیش از ۳ درخواست دریافت شود، درخواست‌های اضافی رد می‌شوند.

**مشکل اصلی:** ترافیک ناگهانی در **لبه‌های پنجره‌های زمانی** می‌تواند باعث عبور تعداد درخواست‌های بیشتر از سهمیه مجاز شود.

![Figure 4-8](design-system/images/System-Design-Interview-page58-image1.jpg)

![Figure 4-9](design-system/images/System-Design-Interview-page59-image1.jpg)

---

###### 📄 صفحه ۶۰

> **Sliding window log algorithm:** The sliding window log algorithm fixes the issue with fixed window counter. It works as follows:
> • The algorithm keeps track of request timestamps. Timestamp data is usually kept in cache, such as sorted sets of Redis [8].
> • When a new request comes in, remove all the outdated timestamps.
> • Add timestamp of the new request to the log.
> • If the log size is the same or lower than the allowed count, a request is accepted. Otherwise, it is rejected.
>
> Pros:
> • Rate limiting implemented by this algorithm is very accurate.
>
> Cons:
> • The algorithm consumes a lot of memory because even if a request is rejected, its timestamp might still be stored in memory.

### الگوریتم Sliding Window Log (گزارش پنجره لغزنده)

این الگوریتم مشکل Fixed Window Counter را حل می‌کند. نحوه عملکرد:

- الگوریتم **زمان‌های درخواست (Timestamps)** را ردیابی می‌کند. داده‌های زمانی معمولاً در کش نگهداری می‌شوند، مانند مجموعه‌های مرتب Redis [۸].

> ***یادداشت شخصی***
>
> 🔗 **ترجمه مقاله:** [ترجمه Rate Limiting بهتر با Redis Sorted Sets](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=BetterRateLimitingWithRedis)
>
> این مقاله ClassDojo نشان می‌دهد چگونه از Sorted Sets Redis برای پیاده‌سازی Rate Limiting توزیع شده با Sliding Window استفاده کنید.

- وقتی درخواست جدیدی می‌رسد، تمام زمان‌های قدیمی حذف می‌شوند.
- زمان درخواست جدید به گزارش اضافه می‌شود.
- اگر اندازه گزارش کمتر یا برابر تعداد مجاز باشد، درخواست پذیرفته می‌شود. در غیر این صورت رد می‌شود.

**مزایا:** Rate Limiting بسیار دقیقی ارائه می‌دهد.
**معایب:** حافظه زیادی مصرف می‌کند، زیرا حتی اگر درخواست رد شود، زمان آن همچنان در حافظه ذخیره می‌شود.

![Figure 4-10](design-system/images/System-Design-Interview-page60-image1.jpg)

![Sliding Window Log Example](design-system/images/System-Design-Interview-page61-image1.jpg)

---

###### 📄 صفحه ۶۱

> **Sliding window counter algorithm:** The sliding window counter algorithm is a hybrid approach that combines the fixed window counter and sliding window log. Assume the rate limiter allows a maximum of 7 requests per minute, and there are 5 requests in the previous minute and 3 in the current minute. For a new request that arrives at a 30% position in the current minute, the number of requests in the rolling window is calculated using the following formula:
>
> Requests in current window + requests in the previous window * overlap percentage of the rolling window and previous window
>
> Using this formula, we get 3 + 5 * 0.7 = 6.5 requests. Depending on the use case, the number can either be rounded up or down. In our example, it is rounded down to 6.
>
> Pros:
> • It smooths out spikes in traffic because the rate is based on the average rate of the previous window.
> • Memory efficient.
>
> Cons:
> • It only works for not-so-strict look back window. It is an approximation of the actual rate.

### الگوریتم Sliding Window Counter (شمارنده پنجره لغزنده)

الگوریتم Sliding Window Counter یک **رویکرد ترکیبی** است که Fixed Window Counter و Sliding Window Log را ترکیب می‌کند.

فرض کنید Rate Limiter حداکثر ۷ درخواست در دقیقه مجاز می‌داند، در دقیقه قبل ۵ درخواست و در دقیقه فعلی ۳ درخواست وجود دارد. برای درخواست جدیدی که در موقعیت ۳۰٪ دقیقه فعلی می‌رسد، تعداد درخواست‌ها با فرمول زیر محاسبه می‌شود:

**تعداد درخواست‌ها در پنجره فعلی + تعداد درخواست‌ها در پنجره قبلی × درصد همپوشانی پنجره لغزنده با پنجره قبلی**

با این فرمول: ۳ + ۵ × ۰.۷ = ۶.۵ درخواست. بسته به مورد کاربری، عدد به بالا یا پایین گرد می‌شود. در مثال ما به ۶ گرد می‌شود. از آنجا که Rate Limiter حداکثر ۷ درخواست مجاز می‌داند، درخواست فعلی پذیرفته می‌شود.

**مزایا:** نوسانات ترافیک را هموار می‌کند و از حافظه بهینه استفاده می‌کند.
**معایب:** فقط برای پنجره‌های بازگشت سخت‌گیرانه نیست کار می‌کند و تقریبی از نرخ واقعی است.

![Figure 4-11](design-system/images/System-Design-Interview-page62-image1.jpg)

---

###### 📄 صفحه ۶۲

> **High-level architecture:** The basic idea of rate limiting algorithms is simple. At the high-level, we need a counter to keep track of how many requests are sent from the same user, IP address, etc. If the counter is larger than the limit, the request is disallowed.
>
> Where shall we store counters? Using the database is not a good idea due to slowness of disk access. In-memory cache is chosen because it is fast and supports time-based expiration strategy. For instance, Redis [11] is a popular option to implement rate limiting. It is an in-memory store that offers two commands: INCR and EXPIRE.
> • INCR: It increases the stored counter by 1.
> • EXPIRE: It sets a timeout for the counter. If the timeout expires, the counter is automatically deleted.
>
> Figure 4-12 shows the high-level architecture for rate limiting, and this works as follows:
> • The client sends a request to rate limiting middleware.
> • Rate limiting middleware fetches the counter from the corresponding bucket in Redis and checks if the limit is reached or not.
> • If the limit is reached, the request is rejected.
> • If the limit is not reached, the request is sent to API servers. Meanwhile, the system increments the counter and saves it back to Redis.

### معماری سطح بالا

ایده اصلی الگوریتم‌های Rate Limiting ساده است. در سطح بالا، به یک **شمارنده** نیاز داریم تا تعداد درخواست‌های ارسال‌شده توسط یک کاربر، آدرس IP و غیره را ردیابی کند. اگر شمارنده از حد مجاز بیشتر شود، درخواست رد می‌شود.

**شمارنده‌ها کجا ذخیره شوند؟** استفاده از پایگاه داده به دلیل کندی دسترسی به دیسک ایده خوبی نیست. از **کش حافظه (In-Memory Cache)** استفاده می‌شود زیرا سریع است و از استراتژی انقضای زمانی پشتیبانی می‌کند. **Redis [۱۱]** گزینه محبوبی برای پیاده‌سازی Rate Limiting است. Redis دو دستور اصلی ارائه می‌دهد:

- **INCR:** شمارنده ذخیره‌شده را ۱ واحد افزایش می‌دهد.
- **EXPIRE:** یک مهلت زمانی برای شمارنده تنظیم می‌کند. اگر مهلت منقضی شود، شمارنده به‌طور خودکار حذف می‌شود.

شکل ۴-۱۲ معماری سطح بالا را نشان می‌دهد و نحوه عملکرد به این صورت است:

- کلاینت درخواستی به میان‌افزار Rate Limiting ارسال می‌کند.
- میان‌افزار شمارنده را از سطل مربوطه در Redis واکشی کرده و بررسی می‌کند آیا حد رسیده است یا خیر.
- اگر حد رسیده باشد، درخواست **رد (Rejected)** می‌شود.
- اگر حد نرسیده باشد، درخواست به سرورهای API ارسال می‌شود و هم‌زمان شمارنده افزایش یافته و در Redis ذخیره می‌شود.

![Figure 4-12](design-system/images/System-Design-Interview-page65-image1.jpg)

---

###### 📄 صفحه ۶۴

> **Step 3 - Design deep dive**
>
> **Rate limiting rules:** Lyft open-sourced their rate-limiting component [12]. Here is an example of rate limiting rules:
> ```
> domain: messaging
> descriptors:
>  - key: message_type
>    Value: marketing
>    rate_limit:
>      unit: day
>      requests_per_unit: 5
> ```
> In the above example, the system is configured to allow a maximum of 5 marketing messages per day.
>
> **Exceeding the rate limit:** In case a request is rate limited, APIs return a HTTP response code 429 (too many requests) to the client.
>
> **Rate limiter headers:** The rate limiter returns the following HTTP headers to clients:
> • X-Ratelimit-Remaining: The remaining number of allowed requests within the window.
> • X-Ratelimit-Limit: It indicates how many calls the client can make per time window.
> • X-Ratelimit-Retry-After: The number of seconds to wait until you can make a request again without being throttled.

### مرحله ۳ - غواصی عمیق در طراحی

**قوانین Rate Limiting:**

شرکت **Lyft** مؤلفه Rate Limiting خود را به صورت متن‌باز منتشر کرده [۱۲]. در ادامه نمونه‌ای از قوانین Rate Limiting آورده شده است:

> ***یادداشت شخصی***
>
> 🔗 **ترجمه و توضیح:** [ترجمه Rate Limiting Lyft](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=LyftRateLimiting)
>
> مخزن GitHub شرکت Lyft که پیاده‌سازی واقعی Rate Limiting با استفاده از Envoy Proxy را نشان می‌دهد.

```yaml
domain: messaging
descriptors:
 - key: message_type
   Value: marketing
   rate_limit:
     unit: day
     requests_per_unit: 5
```

در مثال بالا، سیستم طوری پیکربندی شده که حداکثر ۵ پیام تبلیغاتی در روز مجاز باشد.

**تجاوز از Rate Limit:** اگر درخواستی Rate Limited شود، API کد پاسخ HTTP **429 (too many requests)** را به کلاینت برمی‌گرداند.

**هدرهای Rate Limiter:**

Rate Limiter هدرهای HTTP زیر را به کلاینت‌ها برمی‌گرداند:

- **X-Ratelimit-Remaining:** تعداد درخواست‌های مجاز باقی‌مانده در پنجره فعلی.
- **X-Ratelimit-Limit:** نشان‌دهنده تعداد فراخوانی‌های مجاز کلاینت در هر پنجره زمانی.
- **X-Ratelimit-Retry-After:** تعداد ثانیه‌هایی که باید منتظر بمانید تا بتوانید بدون محدودیت درخواست ارسال کنید.

---

###### 📄 صفحه ۶۵

> **Detailed design:** Figure 4-13 presents a detailed design of the system.
> • Rules are stored on the disk. Workers frequently pull rules from the disk and store them in the cache.
> • When a client sends a request to the server, the request is sent to the rate limiter middleware first.
> • Rate limiter middleware loads rules from the cache. It fetches counters and last request timestamp from Redis cache. Based on the response, the rate limiter decides:
>   • if the request is not rate limited, it is forwarded to API servers.
>   • if the request is rate limited, the rate limiter returns 429 too many requests error to the client. In the meantime, the request is either dropped or forwarded to the queue.

### طراحی تفصیلی

شکل ۴-۱۳ طراحی تفصیلی سیستم را نشان می‌دهد:

- قوانین روی دیسک ذخیره می‌شوند. Workerها به‌طور مکرر قوانین را از دیسک واکشی کرده و در کش ذخیره می‌کنند.
- وقتی کلاینت درخواستی به سرور ارسال می‌کند، درخواست ابتدا به میان‌افزار Rate Limiting ارسال می‌شود.
- میان‌افزار قوانین را از کش بارگذاری می‌کند و شمارنده‌ها و زمان آخرین درخواست را از کش Redis واکشی می‌کند. بر اساس پاسخ، Rate Limiter تصمیم می‌گیرد:
  - اگر درخواست Rate Limited نشده باشد، به سرورهای API ارسال می‌شود.
  - اگر Rate Limited شده باشد، خطای **429 too many requests** به کلاینت برگردانده می‌شود. هم‌زمان درخواست رد یا به صف هدایت می‌شود.

![Figure 4-13](design-system/images/System-Design-Interview-page66-image1.jpg)

---

###### 📄 صفحه ۶۶

> **Rate limiter in a distributed environment:** Building a rate limiter that works in a single server environment is not difficult. However, scaling the system to support multiple servers and concurrent threads is a different story. There are two challenges:
> • Race condition
> • Synchronization issue
>
> **Race condition:** Race conditions can happen in a highly concurrent environment as shown in Figure 4-14. Assume the counter value in Redis is 3. If two requests concurrently read the counter value before either of them writes the value back, each will increment the counter by one and write it back without checking the other thread. Both requests (threads) believe they have the correct counter value 4. However, the correct counter value should be 5.
>
> Locks are the most obvious solution for solving race condition. However, locks will significantly slow down the system. Two strategies are commonly used to solve the problem: Lua script [13] and sorted sets data structure in Redis [8].

### Rate Limiting در محیط توزیع‌شده

ساخت Rate Limiter در محیط تک‌سروری دشوار نیست، اما مقیاس‌دهی برای پشتیبانی از چندین سرور و نخ‌های همزمان (Concurrent Threads) داستان متفاوتی است. **دو چالش اصلی** وجود دارد:

**۱. شرایط مسابقه‌ای (Race Condition):**

شرایط مسابقه‌ای می‌تواند در محیط‌های بسیار همزمان رخ دهد (شکل ۴-۱۴). فرض کنید مقدار شمارنده در Redis برابر ۳ است. اگر دو درخواست به‌طور همزمان مقدار شمارنده را بخوانند قبل از اینکه هرکدام مقدار را بنویسند، هرکدام شمارنده را یک واحد افزایش داده و بدون بررسی نخ دیگر مقدار را برمی‌گردانند. هر دو درخواست فکر می‌کنند مقدار صحیح شمارنده ۴ است، در حالی که مقدار صحیح باید ۵ باشد.

**قفل‌ها (Locks)** بدیهی‌ترین راه‌حل برای شرایط مسابقه‌ای هستند، اما سیستم را به‌طور قابل توجهی کند می‌کنند. دو استراتژی رایج برای حل این مشکل عبارت‌اند از: **Lua Script [۱۳]** و **ساختار داده مجموعه‌های مرتب در Redis [۸]**.

![Figure 4-14](design-system/images/System-Design-Interview-page67-image1.jpg)

---

###### 📄 صفحه ۶۷

> **Synchronization issue:** Synchronization is another important factor to consider in a distributed environment. To support millions of users, one rate limiter server might not be enough to handle the traffic. When multiple rate limiter servers are used, synchronization is required. For example, on the left side of Figure 4-15, client 1 sends requests to rate limiter 1, and client 2 sends requests to rate limiter 2. As the web tier is stateless, clients can send requests to a different rate limiter as shown on the right side of Figure 4-15. If no synchronization happens, rate limiter 1 does not contain any data about client 2. Thus, the rate limiter cannot work properly.
>
> One possible solution is to use sticky sessions that allow a client to send traffic to the same rate limiter. This solution is not advisable because it is neither scalable nor flexible. A better approach is to use centralized data stores like Redis. The design is shown in Figure 4-16.

**۲. مشکل همگام‌سازی (Synchronization Issue):**

همگام‌سازی عامل مهم دیگری در محیط توزیع‌شده است. برای پشتیبانی از میلیون‌ها کاربر، ممکن است یک سرور Rate Limiting کافی نباشد. وقتی از چند سرور Rate Limiting استفاده می‌شود، **همگام‌سازی ضروری** است.

در شکل ۴-۱۵، کلاینت ۱ به Rate Limiter ۱ و کلاینت ۲ به Rate Limiter ۲ درخواست ارسال می‌کند. از آنجا که لایه وب Stateless است، کلاینت‌ها ممکن است به Rate Limiter دیگری درخواست ارسال کنند. اگر همگام‌سازی رخ ندهد، Rate Limiter ۱ هیچ اطلاعاتی درباره کلاینت ۲ ندارد و نمی‌تواند به‌درستی عمل کند.

راه‌حل بهتر استفاده از **فروشگاه‌های داده متمرکز مانند Redis** است (شکل ۴-۱۶).

![Figure 4-15](design-system/images/System-Design-Interview-page67-image2.jpg)

![Figure 4-16](design-system/images/System-Design-Interview-page68-image1.jpg)

---

###### 📄 صفحه ۶۸

> **Performance optimization:** Performance optimization is a common topic in system design interviews. We will cover two areas to improve.
>
> First, multi-data center setup is crucial for a rate limiter because latency is high for users located far away from the data center. Most cloud service providers build many edge server locations around the world. For example, as of 5/20 2020, Cloudflare has 194 geographically distributed edge servers [14]. Traffic is automatically routed to the closest edge server to reduce latency.
>
> Second, synchronize data with an eventual consistency model.

### بهینه‌سازی عملکرد

بهینه‌سازی عملکرد موضوع رایجی در مصاحبه‌های طراحی سیستم است. دو حوزه بهبود را پوشش می‌دهیم:

**۱. راه‌اندازی چند مرکز داده (Multi-Data Center Setup):** این موضوع برای Rate Limiter حیاتی است زیرا Latency برای کاربرانی که از مرکز داده دور هستند بالاست. اکثر ارائه‌دهندگان خدمات ابری مکان‌های زیادی برای سرورهای لبه (Edge Server) در سراسر جهان ایجاد کرده‌اند. برای مثال، Cloudflare تا مه ۲۰۲۰ دارای ۱۹۴ سرور لبه توزیع‌شده جغرافیایی بود [۱۴]. ترافیک به‌طور خودکار به نزدیک‌ترین سرور لبه هدایت می‌شود.

> ***یادداشت شخصی***
>
> 🔗 **ترجمه مقاله Cloudflare:** [ترجمه Rate Limiting در Cloudflare](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=CloudflareRateLimiting)
>
> این مقاله Cloudflare توضیح می‌دهد چگونه Rate Limiting را برای میلیون‌ها دامنه با استفاده از anycast و Sliding Window پیاده‌سازی کرده‌اند.

**۲. همگام‌سازی داده‌ها با مدل سازگاری نهایی (Eventual Consistency Model).**

---

###### 📄 صفحه ۶۸ (ادامه)

> **Monitoring:** After the rate limiter is put in place, it is important to gather analytics data to check whether the rate limiter is effective. Primarily, we want to make sure:
> • The rate limiting algorithm is effective.
> • The rate limiting rules are effective.
>
> For example, if rate limiting rules are too strict, many valid requests are dropped. In this case, we want to relax the rules a little bit. In another example, we notice our rate limiter becomes ineffective when there is a sudden increase in traffic like flash sales. In this scenario, we may replace the algorithm to support burst traffic. Token bucket is a good fit here.

### نظارت (Monitoring)

پس از راه‌اندازی Rate Limiter، جمع‌آوری داده‌های تحلیلی برای بررسی اثربخشی آن مهم است. عمدتاً می‌خواهیم مطمئن شویم:

- الگوریتم Rate Limiting مؤثر است.
- قوانین Rate Limiting مؤثر هستند.

برای مثال، اگر قوانین خیلی سخت‌گیرانه باشند، درخواست‌های معتبر زیادی رد می‌شوند. در این حالت باید قوانین را کمی شل‌تر کنیم. در مثال دیگر، Rate Limiter ممکن است در شرایط افزایش ناگهانی ترافیک مانند **فروش‌های فلش (Flash Sales)** ناکارآمد شود. در این سناریو ممکن است الگوریتم را جایگزین کنیم تا از ترافیک ناگهانی پشتیبانی کند. **Token Bucket** اینجا گزینه مناسبی است.

---

###### 📄 صفحه ۶۹

> **Step 4 - Wrap up**
>
> In this chapter, we discussed different algorithms of rate limiting and their pros/cons. Algorithms discussed include:
> • Token bucket
> • Leaking bucket
> • Fixed window
> • Sliding window log
> • Sliding window counter
>
> Then, we discussed the system architecture, rate limiter in a distributed environment, performance optimization and monitoring. Similar to any system design interview questions, there are additional talking points you can mention if time allows:
> • Hard vs soft rate limiting.
>   • Hard: The number of requests cannot exceed the threshold.
>   • Soft: Requests can exceed the threshold for a short period.
> • Rate limiting at different levels. In this chapter, we only talked about rate limiting at the application level (HTTP: layer 7). It is possible to apply rate limiting at other layers. For example, you can apply rate limiting by IP addresses using Iptables [15] (IP: layer 3).
> • Avoid being rate limited. Design your client with best practices:
>   • Use client cache to avoid making frequent API calls.
>   • Understand the limit and do not send too many requests in a short time frame.
>   • Include code to catch exceptions or errors so your client can gracefully recover from exceptions.
>   • Add sufficient back off time to retry logic.

### مرحله ۴ - جمع‌بندی

در این فصل، الگوریتم‌های مختلف Rate Limiting و مزایا/معایب آن‌ها را بررسی کردیم. الگوریتم‌های مورد بحث شامل Token Bucket، Leaking Bucket، Fixed Window، Sliding Window Log و Sliding Window Counter بودند.

سپس معماری سیستم، Rate Limiting در محیط توزیع‌شده، بهینه‌سازی عملکرد و نظارت را بررسی کردیم.

**نکات تکمیلی:**

- **Rate Limiting سخت در مقابل نرم:**
  - **سخت (Hard):** تعداد درخواست‌ها نمی‌تواند از آستانه تجاوز کند.
  - **نرم (Soft):** درخواست‌ها می‌توانند برای مدت کوتاهی از آستانه تجاوز کنند.

- **Rate Limiting در سطوح مختلف:** در این فصل فقط درباره Rate Limiting در سطح اپلیکیشن (HTTP: لایه ۷) صحبت کردیم. امکان اعمال Rate Limiting در لایه‌های دیگر نیز وجود دارد. برای مثال، می‌توان با استفاده از Iptables [۱۵] بر اساس آدرس IP Rate Limiting اعمال کرد (IP: لایه ۳).

> ***یادداشت شخصی***
>
> 🔗 **ترجمه مقاله:** [ترجمه Rate Limiting با Iptables](https://mdabagh.github.io/blog/post.html?cat=TIL&slug=RateLimitIptables)
>
> این مقاله نشان می‌دهد چگونه Rate Limiting را در لایه ۳ شبکه با استفاده از iptables در لینوکس اعمال کنید.

- **نکته Cloudflare [۱۰]:** Cloudflare مقاله مفصلی درباره نحوه پیاده‌سازی Rate Limiting برای میلیون‌ها دامنه منتشر کرده است.

- **جلوگیری از Rate Limited شدن:** کلاینت خود را بهترین شکل طراحی کنید:
  - از کش کلاینت برای جلوگیری از فراخوانی‌های مکرر API استفاده کنید.
  - حد را درک کنید و در بازه زمانی کوتاه درخواست‌های زیادی ارسال نکنید.
  - کدی برای گرفتن استثناها و خطاها اضافه کنید تا کلاینت شما بتواند به‌نرمی از استثناها بهبود یابد.
  - زمان **Back Off** کافی به منطق تلاش مجدد (Retry Logic) اضافه کنید.

تبریک! تا اینجا پیش رفتید. حالا به خودتان یک آفرین بگویید. آفرین!

---

### مواد مرجع

[۱] Rate-limiting strategies and techniques: https://cloud.google.com/solutions/rate-limiting-strategies-techniques
[۲] Twitter rate limits: https://developer.twitter.com/en/docs/basics/rate-limits
[۳] Google docs usage limits: https://developers.google.com/docs/api/limits
[۴] IBM microservices: https://www.ibm.com/cloud/learn/microservices
[۵] Throttle API requests for better throughput: https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html
[۶] Stripe rate limiters: https://stripe.com/blog/rate-limiters
[۷] Shopify REST Admin API rate limits: https://help.shopify.com/en/api/reference/rest-admin-api-rate-limits
[۸] Better Rate Limiting With Redis Sorted Sets: https://engineering.classdojo.com/blog/2015/02/06/rolling-rate-limiter/
[۹] System Design - Rate limiter and Data modelling: https://medium.com/@saisandeepmopuri/system-design-rate-limiter-and-data-modelling-9304b0d18250
[۱۰] How we built rate limiting capable of scaling to millions of domains: https://blog.cloudflare.com/counting-things-a-lot-of-different-things/
[۱۱] Redis website: https://redis.io/
[۱۲] Lyft rate limiting: https://github.com/lyft/ratelimit
[۱۳] Scaling your API with rate limiters: https://gist.github.com/ptarjan/e38f45f2dfe601419ca3af937fff574d#request-rate-limiter
[۱۴] What is edge computing: https://www.cloudflare.com/learning/serverless/glossary/what-is-edge-computing/
[۱۵] Rate Limit Requests with Iptables: https://blog.programster.org/rate-limit-requests-with-iptables
[۱۶] OSI model: https://en.wikipedia.org/wiki/OSI_model#Layer_architecture
