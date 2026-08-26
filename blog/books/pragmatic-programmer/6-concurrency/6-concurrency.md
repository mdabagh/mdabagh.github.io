> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۲۰۷

> Temporal coupling is when two components of a system must execute in a particular order.
> Identify Concurrency Hazards: Look for shared state, race conditions, and deadlocks.
> Be Explicit About Concurrency: Use languages and frameworks that make concurrency explicit.

جفت‌شدگی زمانی زمانی است که دو مولفه سیستم باید به ترتیب خاصی اجرا شوند.
خطرات همزمانی را شناسایی کنید: به دنبال وضعیت مشترک، شرایط مسابقه و بن‌بست باشید.
درباره همزمانی صریح باشید: از زبان‌ها و چارچوب‌هایی استفاده کنید که همزمانی را صریح می‌کنند.

![Section](images/page001-207.png)

![Section](images/page002-208.png)

![Section](images/page003-209.png)

![Section](images/page004-210.png)

---

###### 📄 صفحه ۲۱۱

> Shared state is a common source of bugs. When multiple threads or processes access the same data, the results can be unpredictable.
> Use Message Passing: Instead of sharing state, share messages.
> Prefer Immutability: Immutable data structures are inherently thread-safe.
> Use Actors or Channels: These provide structured ways to manage concurrent access to state.

وضعیت مشترک منبع رایج باگ‌هاست. وقتی رشته‌ها یا فرآیندهای متعدد به داده‌های یکسان دسترسی دارند، نتایج می‌تواند غیرقابل پیش‌بینی باشد.
از ارسال پیام استفاده کنید: به جای اشتراک‌گذاری وضعیت، پیام‌ها را اشتراک‌گذاری کنید.
تغییرناپذیری را ترجیح دهید: ساختارهای داده تغییرناپذیر ذاتاً thread-safe هستند.

![Section](images/page005-211.png)

![Section](images/page006-212.png)

![Section](images/page007-213.png)

![Section](images/page008-214.png)

---

###### 📄 صفحه ۲۱۵

> Actors are independent units of computation that communicate through message passing.
> Each actor has its own state and processes messages sequentially.
> Actors can create other actors and send messages to other actors.
> This model eliminates many concurrency problems by design.

بازیگران واحدهای مستقل محاسباتی هستند که از طریق ارسال پیام ارتباط برقرار می‌کنند.
هر بازیگر وضعیت خود را دارد و پیام‌ها را به ترتیب پردازش می‌کند.
بازیگران می‌توانند بازیگران دیگری ایجاد کنند و پیام‌هایی به بازیگران دیگر بفرستند.
این مدل بسیاری از مشکلات همزمانی را با طراحی حذف می‌کند.

![Section](images/page009-215.png)

![Section](images/page010-216.png)

![Section](images/page011-217.png)

![Section](images/page012-218.png)

---

###### 📄 صفحه ۲۱۹

> Blackboards provide a shared workspace where multiple agents can read and write information.
> They decouple the producers of information from the consumers.
> Different agents can work on the same problem independently, contributing their findings to the blackboard.

تابلوهای سیاه فضای کار مشترکی فراهم می‌کنند که در آن عوامل متعدد می‌توانند اطلاعات را بخوانند و بنویسند.
آن‌ها تولیدکنندگان اطلاعات را از مصرف‌کنندگان جدا می‌کنند.

![Section](images/page013-219.png)

![Section](images/page014-220.png)

![Section](images/page015-221.png)

![Section](images/page016-222.png)

---
