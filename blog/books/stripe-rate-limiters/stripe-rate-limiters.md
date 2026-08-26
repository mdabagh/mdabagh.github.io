> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: مقیاس‌بندی API شما با Rate Limiterها

> **مقاله اصلی:** Scaling your API with rate limiters
> **نویسنده:** Paul Tarjan (Stripe Engineering)
> **تاریخ انتشار:** March 30, 2017
> **منبع:** https://stripe.com/blog/rate-limiters

---

## چکیده

> Availability and reliability are paramount for all web applications and APIs. If you're providing an API, chances are you've already experienced sudden increases in traffic that affect the quality of your service, potentially even leading to a service outage for all your users.

در دسترس بودن و قابلیت اطمینان برای تمام برنامه‌های کاربردی وب و APIها بسیار حیاتی است. اگر شما یک API ارائه می‌دهید، احتمالاً قبلاً افزایش‌های ناگهانی ترافیک را تجربه کرده‌اید که کیفیت سرویس شما را تحت تأثیر قرار می‌دهد و حتی ممکن است منجر به قطعی سرویس برای تمام کاربران شود.

> Rate limiting can help make your API more reliable in the following scenarios:
> - One of your users is responsible for a spike in traffic, and you need to stay up for everyone else.
> - One of your users has a misbehaving script which is accidentally sending you a lot of requests.
> - A user is sending you a lot of lower-priority requests, and you want to make sure that it doesn't affect your high-priority traffic.

Rate Limiting می‌تواند به قابل اطمینان‌تر شدن API شما در سناریوهای زیر کمک کند:
- یکی از کاربران شما مسئول افزایش ناگهانی ترافیک است و شما باید برای بقیه بالا باشید.
- یکی از کاربران شما اسکریپت نادرستی دارد که درخواست‌های زیادی برای شما ارسال می‌کند.
- کاربری درخواست‌های زیادی با اولویت پایین برای شما ارسال می‌کند و می‌خواهید مطمئن شوید که بر ترافیک با اولویت بالای شما تأثیر نمی‌گذارد.

---

## Rate Limiterها و Load Shedderها

> A *rate limiter* is used to control the rate of traffic sent or received on the network. When should you use a rate limiter? If your users can afford to change the pace at which they hit your API endpoints without affecting the outcome of their requests, then a rate limiter is appropriate.

**Rate Limiter** برای کنترل نرخ ترافیک ارسال یا دریافت شده در شبکه استفاده می‌شود. چه زمانی باید از Rate Limiter استفاده کنید؟ اگر کاربران شما می‌توانند سرعت درخواست به endpointهای API خود را تغییر دهند بدون اینکه بر نتیجه درخواست‌هایشان تأثیر بگذارد، Rate Limiter مناسب است.

> A *load shedder* makes its decisions based on the whole state of the system rather than the user who is making the request. Load shedders help you deal with emergencies.

**Load Shedder** تصمیمات خود را بر اساس کل حالت سیستم اتخاذ می‌کند، نه کاربری که درخواست می‌دهد. Load Shedderها به شما کمک می‌کنند با شرایط اضطراری مقابله کنید.

---

## چهار نوع Rate Limiter در Stripe

### ۱. Request Rate Limiter

> This rate limiter restricts each user to *N* requests per second. Request rate limiters are the first tool most APIs can use to effectively manage a high volume of traffic.

این Rate Limiter هر کاربر را به **N درخواست در ثانیه** محدود می‌کند. Request Rate Limiterها اولین ابزاری هستند که بیشتر APIها می‌توانند برای مدیریت مؤثر ترافیک زیاد استفاده کنند.

### ۲. Concurrent Requests Limiter

> Instead of "You can use our API 1000 times a second", this rate limiter says "You can only have 20 API requests in progress at the same time". Some endpoints are much more resource-intensive than others.

به جای اینکه بگویید "می‌توانید ۱۰۰۰ بار در ثانیه از API ما استفاده کنید"، این Rate Limiter می‌گوید "فقط می‌توانید ۲۰ درخواست API همزمان در حال انجام داشته باشید". برخی endpointها بسیار منابع‌برتر از بقیه هستند.

### ۳. Fleet Usage Load Shedder

> Using this type of load shedder ensures that a certain percentage of your fleet will always be available for your most important API requests.

استفاده از این نوع Load Shedder تضمین می‌کند که درصد مشخصی از ناوگان شما همیشه برای مهم‌ترین درخواست‌های API شما در دسترس خواهد بود.

### ۴. Worker Utilization Load Shedder

> Most API services use a set of workers to independently respond to incoming requests in a parallel fashion. This load shedder is the final line of defense.

بیشتر سرویس‌های API از مجموعه‌ای از Workerها برای پاسخگویی مستقل به درخواست‌های ورودی به صورت موازی استفاده می‌کنند. این Load Shedder آخرین خط دفاعی است.

---

## پیاده‌سازی Rate Limiterها

> We use the [token bucket algorithm](https://en.wikipedia.org/wiki/Token_bucket) to do rate limiting. We implement our rate limiters using Redis.

ما از **الگوریتم Token Bucket** برای انجام Rate Limiting استفاده می‌کنیم. Rate Limiterهای خود را با استفاده از **Redis** پیاده‌سازی می‌کنیم.

> Important things to consider when implementing rate limiters:
> - Hook the rate limiters into your middleware stack safely.
> - Show clear exceptions to your users.
> - Build in safeguards so that you can turn off the limiters.
> - Dark launch each rate limiter to watch the traffic they would block.

نکات مهم هنگام پیاده‌سازی Rate Limiterها:
- Rate Limiterها را به طور ایمن به پشته middleware خود متصل کنید.
- استثنائات واضحی به کاربران خود نشان دهید.
- حفاظ‌هایی بسازید تا بتوانید Limiterها را غیرفعال کنید.
- هر Rate Limiter را به صورت Dark Launch کنید تا ترافیکی که مسدود می‌کند را مشاهده کنید.

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله یکی از بهترین منابع برای درک Rate Limiting در مقیاس واقعی است. Stripe چهار نوع مختلف Rate Limiter را توضیح می‌دهد که هر کدام برای هدف خاصی طراحی شده‌اند.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Stripe Blog - Rate Limiters](https://stripe.com/blog/rate-limiters)
