> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: Rate Limiting بهتر با مجموعه‌های مرتب Redis

> **مقاله اصلی:** Better Rate Limiting With Redis Sorted Sets
> **نویسندگان:** ClassDojo Engineering Team
> **تاریخ انتشار:** February 6, 2015
> **منبع:** https://engineering.classdojo.com/blog/2015/02/06/rolling-rate-limiter/

---

## چکیده

> At ClassDojo, we've recently been building out our push notification infrastructure. Our plans required a rate limiter that met the following criteria:
> - **Distributed**: The rate limiter can be shared across multiple processes.
> - **Rolling Window**: If we set a maximum of 10 messages per minute, we didn't want a user to be able to receive 10 messages at 0:59 and 10 more messages at 1:01.
> - **Minimum Distance Between Messages**: We wanted to enforce a minimum distance between consecutive messages.

در ClassDojo، ما اخیراً زیرساخت اعلان‌های فشاری خود را ساخته‌ایم. برنامه‌های ما به Rate Limiterی نیاز داشت که معیارهای زیر را برآورده کند:
- **توزیع شده:** Rate Limiter باید بین چندین فرآیند مشترک باشد.
- **پنجره لغزان:** اگر حداکثر ۱۰ پیام در دقیقه تنظیم کنیم، نمی‌خواهیم کاربری بتواند ۱۰ پیام در ساعت ۰:۵۹ و ۱۰ پیام دیگر در ساعت ۱:۰۱ دریافت کند.
- **حداقل فاصله بین پیام‌ها:** می‌خواستیم حداقل فاصله بین پیام‌های متوالی را اعمال کنیم.

---

## تلاش اول: Token Bucket

> The canonical algorithm for rate limiting with a rolling window is a token bucket. Here's how it works:
> - Each user has a bucket associated with them, containing a number of tokens.
> - When a user attempts to take an action, we check the number of tokens in the bucket.
> - If the bucket is empty, the user has exceeded the rate, and the action is blocked.

الگوریتم کلاسیک برای Rate Limiting با پنجره لغزان، **Token Bucket** است. نحوه کار آن:
- هر کاربر سطلی مرتبط با خود دارد که تعدادی توکن در آن قرار دارد.
- وقتی کاربر سعی می‌کند عملی انجام دهد، تعداد توکن‌ها در سطل را بررسی می‌کنیم.
- اگر سطل خالی باشد، کاربر از نرخ عبور کرده و عملیات مسدود می‌شود.

> Unfortunately, this algorithm also has a problem: it fails when two processes need to share the rate limiter. Redis can batch operations into one atomic action, but to calculate how many tokens we need to give the user, we need at least two trips to redis.

متأسفانه، این الگوریتم **هم** مشکلی دارد: وقتی دو فرآیند نیاز به اشتراک‌گذاری Rate Limiter دارند، ناکام می‌ماند. Redis می‌تواند عملیات را در یک عمل اتمی گروه‌بندی کند، اما برای محاسبه تعداد توکن‌هایی که باید به کاربر بدهیم، حداقل به دو سفر به redis نیاز داریم.

---

## رویکرد بهتر: مجموعه‌های مرتب

> Fortunately, Redis has another data structure that we can use to prevent these race conditions – the sorted set. Here's the algorithm we came up with:
> - Each user has a sorted set associated with them.
> - When a user attempts to perform an action, we first drop all elements of the set which occurred before one interval ago.
> - We fetch all elements of the set.
> - We add the current timestamp to the set.
> - We set a TTL equal to the rate-limiting interval on the set.
> - After all operations are completed, we count the number of fetched elements.

خوشبختانه، Redis ساختار داده دیگری دارد که می‌توانیم برای جلوگیری از شرایط مسابقه از آن استفاده کنیم – **مجموعه مرتب (Sorted Set)**. الگوریتمی که به آن رسیدیم:
- هر کاربر مجموعه مرتبی مرتبط با خود دارد.
- وقتی کاربر سعی می‌کند عملی انجام دهد، ابتدا تمام عناصر مجموعه را که قبل از یک بازه زمانی رخ داده‌اند حذف می‌کنیم.
- تمام عناصر مجموعه را دریافت می‌کنیم.
- برچسب زمانی فعلی را به مجموعه اضافه می‌کنیم.
- TTL برابر با بازه Rate Limiting روی مجموعه تنظیم می‌کنیم.
- پس از تکمیل تمام عملیات، تعداد عناصر دریافت شده را می‌شماریم.

> The advantage of this approach is that all Redis operations can be performed as an atomic action, using the MULTI command.

مزیت این رویکرد این است که تمام عملیات Redis می‌توانند به عنوان یک عمل اتمی با استفاده از دستور **MULTI** انجام شوند.

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله نشان می‌دهد چگونه **Sorted Sets** در Redis می‌توانند برای پیاده‌سازی Rate Limiting توزیع شده و ایمن از شرایط مسابقه استفاده شوند. الگوریتم Sliding Window با استفاده از ZREMRANGEBYSCORE و ZADD بسیار کارآمد است.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۸/۲۶
**منبع اصلی:** [ClassDojo Engineering Blog](https://engineering.classdojo.com/blog/2015/02/06/rolling-rate-limiter/)
