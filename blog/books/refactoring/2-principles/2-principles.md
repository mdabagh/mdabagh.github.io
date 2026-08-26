> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۵۷

> This chapter shows a progression of refactorings to a sample program. It starts with a fairly simple piece of code for calculating the amount to bill a theater for plays over a season. As we go through refactorings, we improve the code's clarity and add features.

این فصل یک پیشرفت از بازآفرینی‌ها را روی یک برنامه نمونه نشان می‌دهد. با یک قطعه کد نسبتاً ساده برای محاسبه مبلغ صورتحساب تئاتر برای نمایش‌ها در یک فصل شروع می‌شود. همان‌طور که بازآفرینی‌ها را انجام می‌دهیم، وضوح کد را بهبود می‌بخشیم و ویژگی‌ها اضافه می‌کنیم.

![Section](images/page001-057-img1.png)

---

###### 📄 صفحه ۵۸

> We start with a function that calculates the amount a theater owes for plays over a season. The function takes a list of plays and a list of invoices, and returns a statement that shows the total amount owed. This example uses the structure of Statement Data, which is extracted from the raw data, and a renderPlainText function to produce a plain text version of the statement.

با تابعی شروع می‌کنیم که مبلغ بدهکاری تئاتر برای نمایش‌ها در یک فصل را محاسبه می‌کند. این تابع یک لیست از نمایش‌ها و یک لیست از صورتحساب‌ها می‌گیرد و بیانیه‌ای برمی‌گرداند که مبلغ کل بدهکاری را نشان می‌دهد.

![Section](images/page002-058.png)

---

###### 📄 صفحه ۵۹

> To begin the refactoring, I need to establish the solid bottom with tests. I'll start by creating tests based on the existing functionality. Then I can begin to refactor safely, running the tests after each change to ensure I haven't broken anything.

برای شروع بازآفرینی، باید پایه محکمی با آزمایش‌ها ایجاد کنم. با ایجاد آزمایش‌هایی بر اساس عملکرد موجود شروع می‌کنم. سپس می‌توانم با خیال راحت بازآفرینی را شروع کنم و بعد از هر تغییر آزمایش‌ها را اجرا کنم تا مطمئن شوم چیزی را نشکسته‌ام.

![Section](images/page003-059.png)

---

###### 📄 صفحه ۶۰

> The first thing I do with a piece of code is figure out how to break it down. I look at the code and ask myself: "What is the intent of this code?" Then I try to extract the intent into a function with a name that says what it does.

اولین کاری که با یک قطعه کد انجام می‌دهم این است که بفهمم چگونه آن را تقسیم کنم. به کد نگاه می‌کنم و از خودم می‌پرسم: «قصد این کد چیست؟» سپس سعی می‌کنم قصد را در تابعی استخراج کنم که نامش بگوید چه کار می‌کند.

![Section](images/page004-060-img1.png)

---

###### 📄 صفحه ۶۱

> I take a piece of code and name it to explain what it does. I extract the code into a function with that name. I then replace the old code with a call to the function. The key here is that the new function says what it does, rather than having to figure that out from the code itself.

یک قطعه کد برمی‌دارم و نامی به آن می‌دهم تا توضیح دهد چه کار می‌کند. کد را در تابعی با آن نام استخراج می‌کنم. سپس کد قدیمی را با فراخوانی تابع جایگزین می‌کنم. نکته کلیدی اینجاست که تابع جدید می‌گوید چه کار می‌کند، به جای اینکه لازم باشد از خود کد فهمید.

![Section](images/page005-061-img1.png)

---

###### 📄 صفحه ۶۲

> Using Extract Function, I create a new function called renderPlainText. I move the code that does the actual rendering into this new function. Now I have a clear separation between the logic that creates the statement data and the logic that formats it for display.

با استفاده از استخراج تابع، تابع جدیدی به نام renderPlainText ایجاد می‌کنم. کدی که رندر واقعی را انجام می‌دهد به این تابع جدید منتقل می‌کنم. اکنون جداسازی واضحی بین منطقی که داده‌های بیانیه را ایجاد می‌کند و منطقی که آن را برای نمایش قالب‌بندی می‌کند، دارم.

![Section](images/page006-062.png)

---

###### 📄 صفحه ۶۳

> When I see data structures where several fields are always passed together, I consider replacing them with an object. This can simplify function signatures and make the code more expressive. It also makes it easier to add new behavior related to that data structure.

وقتی ساختارهای داده‌ای می‌بینم که چند فیلد همیشه با هم پاس داده می‌شوند، جایگزینی آن‌ها با یک شیء را در نظر می‌گیرم. این می‌تواند امضای تابع را ساده کند و کد را بیانگرتر سازد.

![Section](images/page007-063.png)

---

###### 📄 صفحه ۶۴

> I can split the statement into two parts: one to compute the data and one to render it. This separation means I can reuse the computation of the data in different ways—by rendering it in HTML, for instance. This is a common pattern: separate the computation from the presentation.

می‌توانم بیانیه را به دو بخش تقسیم کنم: یکی برای محاسبه داده‌ها و دیگری برای رندر کردن آن. این جداسازی به این معنی است که می‌توانم محاسبه داده‌ها را به شیوه‌های مختلف بازاستفاده کنم—مثلاً با رندر کردن آن در HTML.

![Section](images/page008-064-img1.png)

---

###### 📄 صفحه ۶۵

> When I have data and functions that operate on them together, I often end up with a class. The statement function creates the data structure and the render functions operate on it. I extract a Statement class from this, encapsulating the data and the rendering together. This encapsulation makes the code much easier to work with, because I can now clearly see what operations are available on the statement data.

وقتی داده‌ها و توابعی دارم که با هم عمل می‌کنند، اغلب به یک کلاس ختم می‌شوم. تابع statement ساختار داده را ایجاد می‌کند و توابع render روی آن عمل می‌کنند. یک کلاس Statement از این‌ها استخراج می‌کنم و داده‌ها و رندرینگ را با هم محصور می‌کنم.

![Section](images/page009-065.png)

---

###### 📄 صفحه ۶۶

> I extract the computation of the charge into its own function. This separates the calculation from the formatting, making both easier to understand and modify independently. The charge function takes a performance and returns a number.

محاسبه هزینه را در تابع مستقل خودش استخراج می‌کنم. این محاسبه را از قالب‌بندی جدا می‌کند و هر دو را آسان‌تر می‌سازد.

![Section](images/page010-066.png)

---

###### 📄 صفحه ۶۷

> Sometimes I find that a function in one class really belongs in another class. When that happens, I use Move Function to put it where it belongs. Or I might find that a method is more naturally expressed as a standalone function.

گاهی اوقات متوجه می‌شوم که تابعی در یک کلاس واقعاً در کلاس دیگری قرار دارد. وقتی این اتفاق می‌افتد، از Move Function استفاده می‌کنم تا آن را به جای خودش ببرم.

![Section](images/page011-067.png)

---

###### 📄 صفحه ۶۸

> This is one of the more important refactorings in the book. I have a function that uses a conditional to select among several behaviors. I replace the conditional with polymorphism, using subclasses or strategy pattern to handle the different cases. This eliminates the conditional logic and makes the code more extensible.

این یکی از مهم‌ترین بازآفرینی‌های کتاب است. تابعی دارم که از شرطی برای انتخاب بین رفتارهای مختلف استفاده می‌کند. شرطی را با پلیمورفیسم جایگزین می‌کنم.

![Section](images/page012-068-img1.png)

---

###### 📄 صفحه ۶۹

> After applying Replace Type Code with Subclasses, I might find that subclasses have different behavior. I extract common behavior into a superclass and let the subclasses provide the variations. This is how inheritance hierarchies evolve.

پس از اعمال جایگزینی کد نوع با زیرکلاس‌ها، ممکن است متوجه شوم زیرکلاس‌ها رفتار متفاوتی دارند.

![Section](images/page013-069.png)

![Section](images/page014-070.png)

![Section](images/page015-071.png)

![Section](images/page016-072.png)

![Section](images/page017-073.png)

![Section](images/page018-074.png)

![Section](images/page019-075.png)

![Section](images/page020-076.png)

![Section](images/page021-077.png)

![Section](images/page022-078.png)

---
