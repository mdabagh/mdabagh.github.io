# فصل ۱۰: ساده‌سازی منطق شرطی



![Simplifying Conditional Logic](images/page001-241-img1.png)

![Simplifying Conditional Logic](images/page004-244.png)

![Simplifying Conditional Logic](images/page007-247.png)

![Simplifying Conditional Logic](images/page010-250.png)

![Simplifying Conditional Logic](images/page013-253.png)

![Simplifying Conditional Logic](images/page016-256.png)

![Simplifying Conditional Logic](images/page019-259.png)

![Simplifying Conditional Logic](images/page022-262.png)

![Simplifying Conditional Logic](images/page025-265.png)

![Simplifying Conditional Logic](images/page028-268.png)

![Simplifying Conditional Logic](images/page031-271.png)

![Simplifying Conditional Logic](images/page034-274.png)

![Simplifying Conditional Logic](images/page037-277-img1.png)

![Simplifying Conditional Logic](images/page040-280.png)

![Simplifying Conditional Logic](images/page043-283.png)

---


⏱️ زمان مطالعه تقریبی: ۴۰ دقیقه

> Conditionals are often the source of complex and hard-to-understand code. This chapter covers techniques for simplifying conditional logic. The key insight is that many conditionals can be eliminated through better design—using polymorphism, decomposing conditions, and removing duplication.

شرطی‌ها اغلب منبع کد پیچیده و سخت قابل فهم هستند. بینش کلیدی این است که بسیاری از شرطی‌ها را می‌توان از طریق طراحی بهتر حذف کرد.

---

### 25. ادغام عبارت شرطی — Consolidate Conditional Expression

> Merges a sequence of tests into a single conditional expression. If I have several if statements that all return the same result and test the same general concept, I can combine them into a single if statement with a combined condition. This makes it clearer that all these conditions represent one idea.

رشته‌ای از آزمون‌ها را در یک عبارت شرطی واحد ادغام می‌کند.

---

### 26. ادغام بخش‌های تکراری شرطی — Consolidate Duplicate Conditional Fragments

> Pulls code out of both branches of a conditional and places it outside. If I find the same code in both the if and else branches, I can move that code outside the conditional, since it will execute regardless.

کد را از هر دو شاخه یک شرطی بیرون می‌کشد و آن را بیرون قرار می‌دهد.

---

### 27. حذف پرچم کنترل — Remove Control Flag

> Replaces a control flag variable with break, continue, or return. If I have a variable that controls the flow of a loop, I can usually replace it with a break, continue, or return statement, making the code clearer.

یک متغیر پرچم کنترل را با break، continue یا return جایگزین می‌کند.

---

### 28. جایگزینی شرطی تودرتو با بسترهای محافظ — Replace Nested Conditional with Guard Clauses

> Replaces a nested conditional with one or more guard clauses. A guard clause is a conditional statement that returns early from a function if it doesn't meet a certain condition. This reduces the nesting level of the code.

شرطی تودرتو را با یک یا چند بستر محافظ جایگزین می‌کند.

---

### 29. جایگزینی شرطی با پلیمورفیسم — Replace Conditional with Polymorphism

> Replaces a conditional that switches on type code with polymorphism. Instead of a big switch statement, I create a subclass for each type. Each subclass overrides the methods that differ. This eliminates the switch and makes it easier to add new types.

شرطی که روی کد نوع سوئیچ می‌زند با پلیمورفیسم جایگزین می‌کند.

---

### 30. معرفی شیء تهی — Introduce Null Object

> Replaces null with a Null Object—a special case object that has the same interface as the normal object but does nothing. This eliminates null checks throughout the code. The Null Object has methods that return sensible defaults instead of null.

null را با یک شیء تهی جایگزین می‌کند—شیء حالت خاصی که رابط یکسانی با شیء عادی دارد اما هیچ کاری انجام نمی‌دهد.

---

### 31. معرفی ادعا — Introduce Assertion

> Makes explicit an assumption that the code makes about the data it works with. An assertion is a conditional statement that should always be true. If it's not, there's a bug. Assertions help document assumptions and catch bugs early.

فرضیه‌ای را که کد درباره داده‌هایی که با آن‌ها کار می‌کند صریحاً بیان می‌کند.

---