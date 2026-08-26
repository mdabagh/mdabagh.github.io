# فصل ۸: انتقال ویژگی‌ها بین اشیاء



![Moving Features](images/page001-191.png)

![Moving Features](images/page003-193.png)

![Moving Features](images/page005-195.png)

![Moving Features](images/page007-197.png)

![Moving Features](images/page009-199-img1.png)

![Moving Features](images/page011-201.png)

![Moving Features](images/page013-203.png)

![Moving Features](images/page015-205.png)

![Moving Features](images/page017-207.png)

![Moving Features](images/page019-209.png)

![Moving Features](images/page021-211.png)

![Moving Features](images/page023-213-img1.png)

![Moving Features](images/page025-215.png)

![Moving Features](images/page027-217-img1.png)

![Moving Features](images/page029-219-img1.png)

---


⏱️ زمان مطالعه تقریبی: ۴۰ دقیقه

> As a program evolves, you'll often find that certain behavior is in the wrong place. A function might be operating on data that belongs to a different class, or a function might be split across two classes when it should be in one. This chapter covers techniques for moving functions and data between classes.

با تکامل برنامه، اغلب متوجه می‌شوید رفتار خاصی در جای اشتباهی قرار دارد.

---

### 15. انتقال تابع — Move Function

> Moves a function into the object it mostly operates on. If a function is using more data from one class than from the one it's in, it should probably be in the other class. This is one of the most common refactorings I perform. The key test is: which class has most of the data the function needs?

تابعی را به شیئی که عمدتاً روی آن عمل می‌کند منتقل می‌کند. اگر تابع از یک کلاس بیشتر از کلاسی که در آن است داده استفاده می‌کند، احتمالاً باید در کلاس دیگر باشد.

---

### 16. انتقال فیلد — Move Field

> Moves a field from one class to another. After a series of changes, a field might end up being used more in another class than in the one it's defined. When that happens, I move it to the class that uses it most.

یک فیلد را از یک کلاس به کلاس دیگر منتقل می‌کند. پس از یک سری تغییرات، یک فیلد ممکن است بیشتر در کلاس دیگری استفاده شود.

---

### 17. انتقال دستورات به تابع — Move Statements into Function

> Takes statements that are the same in several functions and pulls them into a function of their own. If I see the same code appearing in multiple functions, I extract it into a shared function.

دستوراتی که در چند تابع یکسان هستند برمی‌دارد و آن‌ها را در تابع جداگانه‌ای قرار می‌دهد.

---

### 18. انتقال دستورات از تابع — Move Statements out of Function

> Takes statements from a function and moves them to the calling function. Sometimes, some code in a function is only used by the caller. When that's the case, I move that code out to the caller.

دستوراتی را از یک تابع برمی‌دارد و به تابع فراخوان منتقل می‌کند.

---

### 19. جایگزینی متد با شیء متد — Replace Method with Method Object

> Turns a method into its own method object, so that local variables become fields on the method object. This is useful when a function has many local variables that make it hard to extract smaller functions. By turning them into fields, I can break the function down step by step.

یک متد را به شیء متد خودش تبدیل می‌کند تا متغیرهای محلی فیلدهایی روی شیء متد شوند. این زمانی مفید است که تابع متغیرهای محلی زیادی دارد که استخراج توابع کوچک‌تر را سخت می‌کند.

---

### 20. جایگزینی شرطی تودرتو با بسترهای محافظ — Replace Nested Conditional with Guard Clauses

> Replaces a nested conditional with a set of guard clauses. Guard clauses are simple if statements that return early from a function. They reduce the nesting level of the code and make the normal case clearer. The key is to handle the exceptional cases first and then handle the normal case.

شرطی تودرتو را با مجموعه‌ای از بسترهای محافظ جایگزین می‌کند. بسترهای محافظ دستورات if ساده‌ای هستند که زودتر از تابع برمی‌گردند.

---