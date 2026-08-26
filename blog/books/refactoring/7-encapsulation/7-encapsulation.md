# فصل ۷: محصورسازی داده‌ها



![Encapsulation](images/page001-161.png)

![Encapsulation](images/page003-163.png)

![Encapsulation](images/page005-165.png)

![Encapsulation](images/page007-167.png)

![Encapsulation](images/page009-169.png)

![Encapsulation](images/page011-171.png)

![Encapsulation](images/page013-173.png)

![Encapsulation](images/page015-175.png)

![Encapsulation](images/page017-177.png)

![Encapsulation](images/page019-179.png)

![Encapsulation](images/page021-181.png)

![Encapsulation](images/page023-183.png)

![Encapsulation](images/page025-185.png)

![Encapsulation](images/page027-187.png)

![Encapsulation](images/page029-189.png)

---


⏱️ زمان مطالعه تقریبی: ۴۵ دقیقه

> Data structures and the functions that operate on them are the core of any program. As programs evolve, data structures tend to grow and become more complex. This chapter covers techniques for encapsulating data, making it easier to change the data structure without affecting the parts of the program that use it.

ساختارهای داده و توابعی که روی آن‌ها عمل می‌کنند هسته هر برنامه‌ای هستند. با تکامل برنامه‌ها، ساختارهای داده تمایل به رشد و پیچیده‌تر شدن دارند.

---

### 8. محصورسازی رکورد — Encapsulate Record

> Replaces a record (like a hash or struct) with a class. A record is a simple data structure with fields and no functions to manipulate the data. By encapsulating it in a class, I can add methods that give me better control over the data. I can also change the representation of the data without affecting code that uses it.

یک رکورد (مانند هش یا ساختار) را با یک کلاس جایگزین می‌کند. رکورد یک ساختار داده ساده با فیلدها و بدون توابع برای دستکاری داده است.

---

### 9. محصورسازی مجموعه — Encapsulate Collection

> Returns a copy or read-only view of a collection, and provides add/remove methods for manipulating the collection. I encapsulate a collection field by hiding the field behind accessor methods, and providing methods to modify the collection. This gives me control over how the collection is modified.

کپی یا نمای فقط-خواندنی یک مجموعه برمی‌گرداند و متدهای افزودن/حذف برای دستکاری مجموعه فراهم می‌کند.

---

### 10. جایگزینی اولیه با شیء — Replace Primitive with Object

> Replaces a primitive variable with a small object. Sometimes I want to use richer features than a simple data type offers. For example, a string that represents a phone number might have methods to extract the area code or format the number. I create a class for it and provide the methods I need.

یک متغیر اولیه را با یک شیء کوچک جایگزین می‌کند. گاهی اوقات می‌خواهم از ویژگی‌های غنی‌تر از آنچه یک نوع داده ساده ارائه می‌دهد استفاده کنم.

---

### 11. جایگزینی کد نوع با زیرکلاس‌ها — Replace Type Code with Subclasses

> Replaces a type code with subclasses. If I have a field that determines the type of an object (like a "type" field), I can create a subclass for each value of that field. Each subclass overrides the behavior that differs. This uses polymorphism instead of conditionals.

یک کد نوع را با زیرکلاس‌ها جایگزین می‌کند. اگر فیلدی دارم که نوع یک شیء را تعیین می‌کند، می‌توانم برای هر مقدار آن فیلد زیرکلاسی ایجاد کنم.

---

### 12. جایگزینی شرطی با پلیمورفیسم — Replace Conditional with Polymorphism

> Replaces conditional logic with polymorphism. Instead of a long chain of if/else or switch statements that check a type code, I create a separate subclass for each type. Each subclass provides its own implementation of the methods that vary by type. This eliminates the switch and makes it easy to add new types.

منطق شرطی را با پلیمورفیسم جایگزین می‌کند. به جای زنجیره طولانی از دستورات if/else یا switch که کد نوع را بررسی می‌کنند، یک زیرکلاس جداگانه برای هر نوع ایجاد می‌کنم.

---

### 13. معرفی حالت خاص — Introduce Special Case

> When you find the same code being run for two different cases, you may be able to consolidate them by creating a special case value. For example, if I have a function that returns null for a default case and a specific object for other cases, I can create a Null Object that provides the default behavior. This eliminates conditional checks for null.

وقتی متوجه می‌شوید همان کد برای دو حالت مختلف اجرا می‌شود، می‌توانید آن‌ها را با ایجاد یک مقدار حالت خاص یکپارچه کنید.

---

### 14. معرفی ادعا — Introduce Assertion

> An assertion is a conditional statement that should always be true at that point in the code. If it's not true, the code has a bug. Assertions are useful for making implicit assumptions explicit. They don't add any new behavior to the code, but they help document what the code assumes to be true.

ادعا شرطی است که باید در آن نقطه از کد همیشه درست باشد. اگر درست نباشد، کد باگ دارد. ادعاها برای آشکار کردن فرضیات ضمنی مفید هستند.

---