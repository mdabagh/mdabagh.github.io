> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۱۱۱

> This chapter covers the most important and most used refactorings. These are the bread and butter of refactoring work. When I'm refactoring, I usually spend most of my time using these techniques. Once you have a good understanding of these, you'll have the foundation to tackle the more complex refactorings in later chapters.

این فصل مهم‌ترین و پرکاربردترین بازآفرینی‌ها را پوشش می‌دهد. این‌ها نان و کره کار بازآفرینی هستند.

![Section](images/page001-111.png)

![Section](images/page002-112.png)

![Section](images/page003-113.png)

![Section](images/page004-114-img1.png)

![Section](images/page005-115.png)

![Section](images/page006-116-img1.png)

---

###### 📄 صفحه ۱۱۷

> The basic refactoring for replacing a block of code with a function call. If you see a comment saying what a block of code does, that's a clue that you should extract it into a function with a name that says the same thing. The key question I ask myself is: "Can I find a name for this function that describes what it does, not just how it does it?" If I can, that's a good sign.

بازآفرینی پایه‌ای برای جایگزینی یک بلوک کد با فراخوانی تابع. اگر توضیحی می‌بینید که می‌گوید یک بلوک کد چه کار می‌کند، این نشانه‌ای است که باید آن را در تابعی با نامی که همان چیز را بگوید استخراج کنید.

**روش اجرا:**
- یک بلوک کد را بیابید که می‌توان آن را در یک تابع جدید گروه‌بندی کرد
- یک نام مناسب برای تابع انتخاب کنید که قصد کد را بیان کند
- پارامترهای لازم را به تابع منتقل کنید
- کد اصلی را با فراخوانی تابع جایگزین کنید
- آزمون‌ها را اجرا کنید

![Section](images/page007-117-img1.png)

![Section](images/page008-118.png)

![Section](images/page009-119.png)

![Section](images/page010-120.png)

![Section](images/page011-121.png)

![Section](images/page012-122-img1.png)

---

###### 📄 صفحه ۱۲۳

> Inlines a function call. This is the inverse of Extract Function. When I see a function whose body is as clear as its name, I inline it. The function call adds no value; it just obscures what's going on. It's like reading a book where every paragraph starts with "In this paragraph, I will explain..."

یک فراخوانی تابع را درج می‌کند. این معکوس استخراج تابع است. وقتی تابعی می‌بینم که بدنه‌اش به اندازه نامش واضح است، آن را درج می‌کنم.

![Section](images/page013-123.png)

![Section](images/page014-124.png)

![Section](images/page015-125.png)

![Section](images/page016-126.png)

![Section](images/page017-127.png)

![Section](images/page018-128.png)

---

###### 📄 صفحه ۱۲۹

> Takes a piece of code that explains the result of an expression and puts it into a well-named variable. This is useful when the expression is long and complex. Giving the result a name makes the code clearer. I also use this when I have the same expression in multiple places—extract it once and use the variable everywhere.

یک قطعه کد که نتیجه یک عبارت را توضیح می‌دهد برمی‌دارد و آن را در متغیری با نام مناسب قرار می‌دهد. این زمانی مفید است که عبارت طولانی و پیچیده است.

![Section](images/page019-129.png)

![Section](images/page020-130.png)

![Section](images/page021-131.png)

![Section](images/page022-132-img1.png)

![Section](images/page023-133.png)

![Section](images/page024-134.png)

---

###### 📄 صفحه ۱۳۵

> Takes a variable, puts its expression into the variable's places, and removes the variable. Inlines a variable. This is the opposite of Extract Variable. If a variable has a short name, and the value is easy to understand, it can be clearer to just use the expression directly.

یک متغیر برمی‌دارد، عبارت آن را در جایگاه‌های متغیر قرار می‌دهد و متغیر را حذف می‌کند. این متضاد استخراج متغیر است.

![Section](images/page025-135.png)

![Section](images/page026-136-img1.png)

![Section](images/page027-137.png)

![Section](images/page028-138.png)

![Section](images/page029-139.png)

![Section](images/page030-140-img1.png)

---

###### 📄 صفحه ۱۴۱

> Makes a simple change to a function signature. I rename a function's parameters, add or remove parameters, or change their order. The key is to make the interface of the function clearer and more convenient to use. This is the rename refactoring for functions.

تغییر ساده‌ای در امضای تابع ایجاد می‌کند. نام پارامترهای تابع را تغییر می‌دهم، پارامترها اضافه یا حذف می‌کنم، یا ترتیب آن‌ها را تغییر می‌دهم.

![Section](images/page031-141-img1.png)

![Section](images/page032-142.png)

![Section](images/page033-143.png)

![Section](images/page034-144.png)

![Section](images/page035-145.png)

![Section](images/page036-146.png)

---

###### 📄 صفحه ۱۴۷

> Replaces a direct variable access with a getter and setter function. This is valuable when you want to control what can modify the variable, and you want to be able to change the internal representation later without affecting the callers. This is like Encapsulate Field, but for variables (both local and field).

دسترسی مستقیم به متغیر را با تابع getter و setter جایگزین می‌کند. این زمانی ارزشمند است که می‌خواهید کنترل کنید چه چیزی می‌تواند متغیر را تغییر دهد.

![Section](images/page037-147.png)

![Section](images/page038-148.png)

![Section](images/page039-149.png)

![Section](images/page040-150-img1.png)

![Section](images/page041-151.png)

![Section](images/page042-152.png)

---

###### 📄 صفحه ۱۵۳

> Changes the name of a variable. This is one of the simplest refactorings, but it can be one of the most valuable. A good variable name can make code much easier to understand. When I rename a variable, I change every reference to it throughout the code base. This is easy for tools to do, so I use a rename tool.

نام متغیر را تغییر می‌دهد. این یکی از ساده‌ترین بازآفرینی‌ها است، اما می‌تواند یکی از ارزشمندترین‌ها باشد.

![Section](images/page043-153.png)

![Section](images/page044-154.png)

![Section](images/page045-155.png)

![Section](images/page046-156-img1.png)

![Section](images/page047-157.png)

![Section](images/page048-158.png)

![Section](images/page049-159-img1.png)

![Section](images/page050-160.png)

---
