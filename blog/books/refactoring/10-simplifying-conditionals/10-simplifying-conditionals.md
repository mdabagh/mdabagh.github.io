> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۲۴۱

> Conditionals are often the source of complex and hard-to-understand code. This chapter covers techniques for simplifying conditional logic. The key insight is that many conditionals can be eliminated through better design—using polymorphism, decomposing conditions, and removing duplication.

شرطی‌ها اغلب منبع کد پیچیده و سخت قابل فهم هستند. بینش کلیدی این است که بسیاری از شرطی‌ها را می‌توان از طریق طراحی بهتر حذف کرد.

![Section](images/page001-241-img1.png)

![Section](images/page002-242.png)

![Section](images/page003-243.png)

![Section](images/page004-244.png)

![Section](images/page005-245-img1.png)

---

###### 📄 صفحه ۲۴۶

> Merges a sequence of tests into a single conditional expression. If I have several if statements that all return the same result and test the same general concept, I can combine them into a single if statement with a combined condition. This makes it clearer that all these conditions represent one idea.

رشته‌ای از آزمون‌ها را در یک عبارت شرطی واحد ادغام می‌کند.

![Section](images/page006-246.png)

![Section](images/page007-247.png)

![Section](images/page008-248.png)

![Section](images/page009-249.png)

![Section](images/page010-250.png)

---

###### 📄 صفحه ۲۵۱

> Pulls code out of both branches of a conditional and places it outside. If I find the same code in both the if and else branches, I can move that code outside the conditional, since it will execute regardless.

کد را از هر دو شاخه یک شرطی بیرون می‌کشد و آن را بیرون قرار می‌دهد.

![Section](images/page011-251-img1.png)

![Section](images/page012-252-img1.png)

![Section](images/page013-253.png)

![Section](images/page014-254.png)

![Section](images/page015-255.png)

---

###### 📄 صفحه ۲۵۶

> Replaces a control flag variable with break, continue, or return. If I have a variable that controls the flow of a loop, I can usually replace it with a break, continue, or return statement, making the code clearer.

یک متغیر پرچم کنترل را با break، continue یا return جایگزین می‌کند.

![Section](images/page016-256.png)

![Section](images/page017-257-img1.png)

![Section](images/page018-258.png)

![Section](images/page019-259.png)

![Section](images/page020-260.png)

---

###### 📄 صفحه ۲۶۱

> Replaces a nested conditional with one or more guard clauses. A guard clause is a conditional statement that returns early from a function if it doesn't meet a certain condition. This reduces the nesting level of the code.

شرطی تودرتو را با یک یا چند بستر محافظ جایگزین می‌کند.

![Section](images/page021-261-img1.png)

![Section](images/page022-262.png)

![Section](images/page023-263.png)

![Section](images/page024-264.png)

![Section](images/page025-265.png)

---

###### 📄 صفحه ۲۶۶

> Replaces a conditional that switches on type code with polymorphism. Instead of a big switch statement, I create a subclass for each type. Each subclass overrides the methods that differ. This eliminates the switch and makes it easier to add new types.

شرطی که روی کد نوع سوئیچ می‌زند با پلیمورفیسم جایگزین می‌کند.

![Section](images/page026-266.png)

![Section](images/page027-267-img1.png)

![Section](images/page028-268.png)

![Section](images/page029-269-img1.png)

![Section](images/page030-270.png)

---

###### 📄 صفحه ۲۷۱

> Replaces null with a Null Object—a special case object that has the same interface as the normal object but does nothing. This eliminates null checks throughout the code. The Null Object has methods that return sensible defaults instead of null.

null را با یک شیء تهی جایگزین می‌کند—شیء حالت خاصی که رابط یکسانی با شیء عادی دارد اما هیچ کاری انجام نمی‌دهد.

![Section](images/page031-271.png)

![Section](images/page032-272.png)

![Section](images/page033-273-img1.png)

![Section](images/page034-274.png)

![Section](images/page035-275.png)

---

###### 📄 صفحه ۲۷۶

> Makes explicit an assumption that the code makes about the data it works with. An assertion is a conditional statement that should always be true. If it's not, there's a bug. Assertions help document assumptions and catch bugs early.

فرضیه‌ای را که کد درباره داده‌هایی که با آن‌ها کار می‌کند صریحاً بیان می‌کند.

![Section](images/page036-276.png)

![Section](images/page037-277-img1.png)

![Section](images/page038-278.png)

![Section](images/page039-279.png)

![Section](images/page040-280.png)

![Section](images/page041-281-img1.png)

![Section](images/page042-282.png)

![Section](images/page043-283.png)

![Section](images/page044-284.png)

![Section](images/page045-285-img1.png)

![Section](images/page046-286.png)

---
