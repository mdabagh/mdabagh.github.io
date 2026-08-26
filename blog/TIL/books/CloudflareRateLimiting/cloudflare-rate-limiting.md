# ترجمه فارسی: چگونه Rate Limiting را برای مقیاس‌بندی تا میلیون‌ها دامنه ساختیم

> **مقاله اصلی:** How we built rate limiting capable of scaling to millions of domains
> **نویسنده:** Cloudflare Team
> **تاریخ انتشار:** June 7, 2017
> **منبع:** https://blog.cloudflare.com/counting-things-a-lot-of-different-things/

---

## چکیده

> Back in April we announced Rate Limiting of requests for every Cloudflare customer. Being able to rate limit at the edge of the network has many advantages: it's easier for customers to set up and operate, their origin servers are not bothered by excessive traffic or layer 7 attacks.

ما Rate Limiting درخواست‌ها را برای هر مشتری Cloudflare اعلام کردیم. توانایی Rate Limiting در لبه شبکه مزایای زیادی دارد: راه‌اندازی و مدیریت آن برای مشتریان آسان‌تر است، سرورهای اصلی آنها توسط ترافیک بیش از حد یا حملات لایه ۷ آزار نمی‌بینند.

> In a nutshell, rate limiting works like this:
> - Customers can define one or more rate limit rules that match particular HTTP requests
> - Every request that matches the rule is counted per client IP address
> - Once that counter exceeds a threshold, further requests are not allowed to reach the origin server

به طور خلاصه، Rate Limiting اینگونه کار می‌کند:
- مشتریان می‌توانند یک یا چند قانون Rate Limit تعریف کنند که درخواست‌های HTTP خاصی را مطابقت دهند
- هر درخواستی که با قانون مطابقت دارد برای هر آدرس IP مشتری شمارش می‌شود
- وقتی آن شمارنده از آستانه فراتر رود، درخواست‌های بعدی اجازه رسیدن به سرور اصلی را ندارند

---

## چالش مقیاس‌بندی

> Doing this with possibly millions of domains and even more millions of rules immediately becomes a bit more complicated.

انجام این کار با احتمالاً میلیون‌ها دامنه و حتی میلیون‌ها قانون بیشتر، فوراً کمی پیچیده‌تر می‌شود.

> Since Cloudflare has a vast and diverse network, reporting all counters to a single central point is not a realistic solution as the latency is far too high.

از آنجا که Cloudflare شبکه گسترده و متنوعی دارد، گزارش تمام شمارنده‌ها به یک نقطه مرکزی واحد راه‌حل واقع‌بینانه‌ای نیست زیرا تأخیر بسیار زیاد است.

> All the traffic going to our edge servers is anycast traffic. This means that we announce the same IP address for a given web application, site or API worldwide, and traffic will be automatically and consistently routed to the closest live data center.

تمام ترافیکی که به سرورهای لبه ما می‌رود، ترافیک **anycast** است. این بدان معناست که ما همان آدرس IP را برای یک برنامه کاربردی وب، سایت یا API در سراسر جهان اعلام می‌کنیم و ترافیک به طور خودکار و مداوم به نزدیک‌ترین مرکز داده فعال مسیریابی می‌شود.

---

## الگوریتم Sliding Window

> The most naive implementation is to simply increment a counter that we reset at the start of each sampling period. This works but is not terribly accurate.

ساده‌ترین پیاده‌سازی این است که به سادگی شمارنده‌ای را افزایش دهیم که در ابتدای هر دوره نمونه‌برداری بازنشانی می‌کنیم. این کار می‌کند اما خیلی دقیق نیست.

> So here we are: we can finally implement a good counting system using only a few memcache primitives and without much contention.

پس ما اینجاییم: بالاخره می‌توانیم یک سیستم شمارش خوب با استفاده از فقط چند عملیات اولیه memcache و بدون رقابت زیاد پیاده‌سازی کنیم.

> This last tweak allowed us to efficiently mitigate large L7 attacks without noticeably penalizing legitimate requests.

این بهینه‌سازی نهایی به ما اجازه داد حملات بزرگ L7 را به طور کارآمد کاهش دهیم بدون اینکه درخواست‌های مشروع را به طور قابل توجهی جریمه کنیم.

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله یکی از بهترین توضیحات در مورد Rate Limiting در مقیاس واقعی است. Cloudflare نشان می‌دهد چگونه با استفاده از **anycast**, **Sliding Window Algorithm** و **Redis**، Rate Limiting را برای میلیون‌ها دامنه پیاده‌سازی کرده‌اند.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [Cloudflare Blog - Rate Limiting](https://blog.cloudflare.com/counting-things-a-lot-of-different-things/)
