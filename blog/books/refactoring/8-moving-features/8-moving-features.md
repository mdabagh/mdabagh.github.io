> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۱۹۱

> As a program evolves, you'll often find that certain behavior is in the wrong place. A function might be operating on data that belongs to a different class, or a function might be split across two classes when it should be in one. This chapter covers techniques for moving functions and data between classes.

با تکامل برنامه، اغلب متوجه می‌شوید رفتار خاصی در جای اشتباهی قرار دارد.

![Section](images/page001-191.png)

![Section](images/page002-192.png)

![Section](images/page003-193.png)

![Section](images/page004-194-img1.png)

---

###### 📄 صفحه ۱۹۵

> Moves a function into the object it mostly operates on. If a function is using more data from one class than from the one it's in, it should probably be in the other class. This is one of the most common refactorings I perform. The key test is: which class has most of the data the function needs?

تابعی را به شیئی که عمدتاً روی آن عمل می‌کند منتقل می‌کند. اگر تابع از یک کلاس بیشتر از کلاسی که در آن است داده استفاده می‌کند، احتمالاً باید در کلاس دیگر باشد.

![Section](images/page005-195.png)

![Section](images/page006-196.png)

![Section](images/page007-197.png)

![Section](images/page008-198.png)

---

###### 📄 صفحه ۱۹۹

> Moves a field from one class to another. After a series of changes, a field might end up being used more in another class than in the one it's defined. When that happens, I move it to the class that uses it most.

یک فیلد را از یک کلاس به کلاس دیگر منتقل می‌کند. پس از یک سری تغییرات، یک فیلد ممکن است بیشتر در کلاس دیگری استفاده شود.

![Section](images/page009-199-img1.png)

![Section](images/page010-200.png)

![Section](images/page011-201.png)

![Section](images/page012-202.png)

---

###### 📄 صفحه ۲۰۳

> Takes statements that are the same in several functions and pulls them into a function of their own. If I see the same code appearing in multiple functions, I extract it into a shared function.

دستوراتی که در چند تابع یکسان هستند برمی‌دارد و آن‌ها را در تابع جداگانه‌ای قرار می‌دهد.

![Section](images/page013-203.png)

![Section](images/page014-204-img1.png)

![Section](images/page015-205.png)

![Section](images/page016-206.png)

---

###### 📄 صفحه ۲۰۷

> Takes statements from a function and moves them to the calling function. Sometimes, some code in a function is only used by the caller. When that's the case, I move that code out to the caller.

دستوراتی را از یک تابع برمی‌دارد و به تابع فراخوان منتقل می‌کند.

![Section](images/page017-207.png)

![Section](images/page018-208-img1.png)

![Section](images/page019-209.png)

![Section](images/page020-210.png)

---

###### 📄 صفحه ۲۱۱

> Turns a method into its own method object, so that local variables become fields on the method object. This is useful when a function has many local variables that make it hard to extract smaller functions. By turning them into fields, I can break the function down step by step.

یک متد را به شیء متد خودش تبدیل می‌کند تا متغیرهای محلی فیلدهایی روی شیء متد شوند. این زمانی مفید است که تابع متغیرهای محلی زیادی دارد که استخراج توابع کوچک‌تر را سخت می‌کند.

![Section](images/page021-211.png)

![Section](images/page022-212.png)

![Section](images/page023-213-img1.png)

![Section](images/page024-214.png)

---

###### 📄 صفحه ۲۱۵

> Replaces a nested conditional with a set of guard clauses. Guard clauses are simple if statements that return early from a function. They reduce the nesting level of the code and make the normal case clearer. The key is to handle the exceptional cases first and then handle the normal case.

شرطی تودرتو را با مجموعه‌ای از بسترهای محافظ جایگزین می‌کند. بسترهای محافظ دستورات if ساده‌ای هستند که زودتر از تابع برمی‌گردند.

![Section](images/page025-215.png)

![Section](images/page026-216-img1.png)

![Section](images/page027-217-img1.png)

![Section](images/page028-218.png)

![Section](images/page029-219-img1.png)

![Section](images/page030-220.png)

![Section](images/page031-221.png)

![Section](images/page032-222-img1.png)

![Section](images/page033-223.png)

![Section](images/page034-224.png)

---
