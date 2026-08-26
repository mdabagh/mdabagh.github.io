# فصل ۶: مجموعه اول بازآفرینی‌ها



![A First Set of Refactorings](images/page001-111.png)

![A First Set of Refactorings](images/page005-115.png)

![A First Set of Refactorings](images/page009-119.png)

![A First Set of Refactorings](images/page013-123.png)

![A First Set of Refactorings](images/page017-127.png)

![A First Set of Refactorings](images/page021-131.png)

![A First Set of Refactorings](images/page025-135.png)

![A First Set of Refactorings](images/page029-139.png)

![A First Set of Refactorings](images/page033-143.png)

![A First Set of Refactorings](images/page037-147.png)

![A First Set of Refactorings](images/page041-151.png)

![A First Set of Refactorings](images/page045-155.png)

![A First Set of Refactorings](images/page049-159-img1.png)

---


⏱️ زمان مطالعه تقریبی: ۶۰ دقیقه

> This chapter covers the most important and most used refactorings. These are the bread and butter of refactoring work. When I'm refactoring, I usually spend most of my time using these techniques. Once you have a good understanding of these, you'll have the foundation to tackle the more complex refactorings in later chapters.

این فصل مهم‌ترین و پرکاربردترین بازآفرینی‌ها را پوشش می‌دهد. این‌ها نان و کره کار بازآفرینی هستند.

---

### 1. استخراج تابع — Extract Function

> The basic refactoring for replacing a block of code with a function call. If you see a comment saying what a block of code does, that's a clue that you should extract it into a function with a name that says the same thing. The key question I ask myself is: "Can I find a name for this function that describes what it does, not just how it does it?" If I can, that's a good sign.

بازآفرینی پایه‌ای برای جایگزینی یک بلوک کد با فراخوانی تابع. اگر توضیحی می‌بینید که می‌گوید یک بلوک کد چه کار می‌کند، این نشانه‌ای است که باید آن را در تابعی با نامی که همان چیز را بگوید استخراج کنید.

**روش اجرا:**
- یک بلوک کد را بیابید که می‌توان آن را در یک تابع جدید گروه‌بندی کرد
- یک نام مناسب برای تابع انتخاب کنید که قصد کد را بیان کند
- پارامترهای لازم را به تابع منتقل کنید
- کد اصلی را با فراخوانی تابع جایگزین کنید
- آزمون‌ها را اجرا کنید

---

### 2. درج تابع — Inline Function

> Inlines a function call. This is the inverse of Extract Function. When I see a function whose body is as clear as its name, I inline it. The function call adds no value; it just obscures what's going on. It's like reading a book where every paragraph starts with "In this paragraph, I will explain..."

یک فراخوانی تابع را درج می‌کند. این معکوس استخراج تابع است. وقتی تابعی می‌بینم که بدنه‌اش به اندازه نامش واضح است، آن را درج می‌کنم.

---

### 3. استخراج متغیر — Extract Variable

> Takes a piece of code that explains the result of an expression and puts it into a well-named variable. This is useful when the expression is long and complex. Giving the result a name makes the code clearer. I also use this when I have the same expression in multiple places—extract it once and use the variable everywhere.

یک قطعه کد که نتیجه یک عبارت را توضیح می‌دهد برمی‌دارد و آن را در متغیری با نام مناسب قرار می‌دهد. این زمانی مفید است که عبارت طولانی و پیچیده است.

---

### 4. درج متغیر — Inline Variable

> Takes a variable, puts its expression into the variable's places, and removes the variable. Inlines a variable. This is the opposite of Extract Variable. If a variable has a short name, and the value is easy to understand, it can be clearer to just use the expression directly.

یک متغیر برمی‌دارد، عبارت آن را در جایگاه‌های متغیر قرار می‌دهد و متغیر را حذف می‌کند. این متضاد استخراج متغیر است.

---

### 5. تغییر اعلان تابع — Change Function Declaration

> Makes a simple change to a function signature. I rename a function's parameters, add or remove parameters, or change their order. The key is to make the interface of the function clearer and more convenient to use. This is the rename refactoring for functions.

تغییر ساده‌ای در امضای تابع ایجاد می‌کند. نام پارامترهای تابع را تغییر می‌دهم، پارامترها اضافه یا حذف می‌کنم، یا ترتیب آن‌ها را تغییر می‌دهم.

---

### 6. محصورسازی متغیر — Encapsulate Variable

> Replaces a direct variable access with a getter and setter function. This is valuable when you want to control what can modify the variable, and you want to be able to change the internal representation later without affecting the callers. This is like Encapsulate Field, but for variables (both local and field).

دسترسی مستقیم به متغیر را با تابع getter و setter جایگزین می‌کند. این زمانی ارزشمند است که می‌خواهید کنترل کنید چه چیزی می‌تواند متغیر را تغییر دهد.

---

### 7. تغییر نام متغیر — Rename Variable

> Changes the name of a variable. This is one of the simplest refactorings, but it can be one of the most valuable. A good variable name can make code much easier to understand. When I rename a variable, I change every reference to it throughout the code base. This is easy for tools to do, so I use a rename tool.

نام متغیر را تغییر می‌دهد. این یکی از ساده‌ترین بازآفرینی‌ها است، اما می‌تواند یکی از ارزشمندترین‌ها باشد.

---