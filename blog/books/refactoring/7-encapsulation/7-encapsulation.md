> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۱۶۱

> Data structures and the functions that operate on them are the core of any program. As programs evolve, data structures tend to grow and become more complex. This chapter covers techniques for encapsulating data, making it easier to change the data structure without affecting the parts of the program that use it.

ساختارهای داده و توابعی که روی آن‌ها عمل می‌کنند هسته هر برنامه‌ای هستند. با تکامل برنامه‌ها، ساختارهای داده تمایل به رشد و پیچیده‌تر شدن دارند.

![Section](images/page001-161.png)

![Section](images/page002-162.png)

![Section](images/page003-163.png)

---

###### 📄 صفحه ۱۶۴

> Replaces a record (like a hash or struct) with a class. A record is a simple data structure with fields and no functions to manipulate the data. By encapsulating it in a class, I can add methods that give me better control over the data. I can also change the representation of the data without affecting code that uses it.

یک رکورد (مانند هش یا ساختار) را با یک کلاس جایگزین می‌کند. رکورد یک ساختار داده ساده با فیلدها و بدون توابع برای دستکاری داده است.

![Section](images/page004-164-img1.png)

![Section](images/page005-165.png)

![Section](images/page006-166.png)

---

###### 📄 صفحه ۱۶۷

> Returns a copy or read-only view of a collection, and provides add/remove methods for manipulating the collection. I encapsulate a collection field by hiding the field behind accessor methods, and providing methods to modify the collection. This gives me control over how the collection is modified.

کپی یا نمای فقط-خواندنی یک مجموعه برمی‌گرداند و متدهای افزودن/حذف برای دستکاری مجموعه فراهم می‌کند.

![Section](images/page007-167.png)

![Section](images/page008-168.png)

![Section](images/page009-169.png)

---

###### 📄 صفحه ۱۷۰

> Replaces a primitive variable with a small object. Sometimes I want to use richer features than a simple data type offers. For example, a string that represents a phone number might have methods to extract the area code or format the number. I create a class for it and provide the methods I need.

یک متغیر اولیه را با یک شیء کوچک جایگزین می‌کند. گاهی اوقات می‌خواهم از ویژگی‌های غنی‌تر از آنچه یک نوع داده ساده ارائه می‌دهد استفاده کنم.

![Section](images/page010-170-img1.png)

![Section](images/page011-171.png)

![Section](images/page012-172.png)

---

###### 📄 صفحه ۱۷۳

> Replaces a type code with subclasses. If I have a field that determines the type of an object (like a "type" field), I can create a subclass for each value of that field. Each subclass overrides the behavior that differs. This uses polymorphism instead of conditionals.

یک کد نوع را با زیرکلاس‌ها جایگزین می‌کند. اگر فیلدی دارم که نوع یک شیء را تعیین می‌کند، می‌توانم برای هر مقدار آن فیلد زیرکلاسی ایجاد کنم.

![Section](images/page013-173.png)

![Section](images/page014-174.png)

![Section](images/page015-175.png)

---

###### 📄 صفحه ۱۷۶

> Replaces conditional logic with polymorphism. Instead of a long chain of if/else or switch statements that check a type code, I create a separate subclass for each type. Each subclass provides its own implementation of the methods that vary by type. This eliminates the switch and makes it easy to add new types.

منطق شرطی را با پلیمورفیسم جایگزین می‌کند. به جای زنجیره طولانی از دستورات if/else یا switch که کد نوع را بررسی می‌کنند، یک زیرکلاس جداگانه برای هر نوع ایجاد می‌کنم.

![Section](images/page016-176-img1.png)

![Section](images/page017-177.png)

![Section](images/page018-178.png)

---

###### 📄 صفحه ۱۷۹

> When you find the same code being run for two different cases, you may be able to consolidate them by creating a special case value. For example, if I have a function that returns null for a default case and a specific object for other cases, I can create a Null Object that provides the default behavior. This eliminates conditional checks for null.

وقتی متوجه می‌شوید همان کد برای دو حالت مختلف اجرا می‌شود، می‌توانید آن‌ها را با ایجاد یک مقدار حالت خاص یکپارچه کنید.

![Section](images/page019-179.png)

![Section](images/page020-180.png)

![Section](images/page021-181.png)

---

###### 📄 صفحه ۱۸۲

> An assertion is a conditional statement that should always be true at that point in the code. If it's not true, the code has a bug. Assertions are useful for making implicit assumptions explicit. They don't add any new behavior to the code, but they help document what the code assumes to be true.

ادعا شرطی است که باید در آن نقطه از کد همیشه درست باشد. اگر درست نباشد، کد باگ دارد. ادعاها برای آشکار کردن فرضیات ضمنی مفید هستند.

![Section](images/page022-182.png)

![Section](images/page023-183.png)

![Section](images/page024-184-img1.png)

![Section](images/page025-185.png)

![Section](images/page026-186.png)

![Section](images/page027-187.png)

![Section](images/page028-188.png)

![Section](images/page029-189.png)

![Section](images/page030-190.png)

---
