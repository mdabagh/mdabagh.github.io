> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
---
title: "بازآفرینی کد: بهبود طراحی کدهای موجود"
author: "مارتین فاولر (Martin Fowler)"
original_title: "Refactoring: Improving the Design of Existing Code (2nd Edition)"
publisher: "Addison-Wesley Professional"
year: "2018"
translator: "ترجمه به فارسی"
tags: [refactoring, design-patterns, clean-code, programming]
---

# بازآفرینی کد: بهبود طراحی کدهای موجود

**نویسنده:** مارتین فاولر (Martin Fowler)  
**ناشر:** Addison-Wesley Professional  
**سال انتشار:** ۲۰۱۸  
**ویرایش دوم**

---

## فهرست مطالب

- [فصل ۱: بازآفرینی — چیستی و چرایی](#فصل-۱-بازآفرینی)
- [فصل ۲: نمونه‌ای از بازآفرینی](#فصل-۲-نمونه‌ای-از-بازآفرینی)
- [فصل ۳: فرهنگ بازآفرینی](#فصل-۳-فرهنگ-بازآفرینی)
- [فصل ۴: شروع کار](#فصل-۴-شروع-کار)
- [فصل ۵: هوشمندتر عمل کردن](#فصل-۵-هوشمندتر-عمل-کردن)
- [فصل ۶: مجموعه اول بازآفرینی‌ها](#فصل-۶-مجموعه-اول-بازآفرینی‌ها)
- [فصل ۷: محصورسازی داده‌ها](#فصل-۷-محصورسازی-داده‌ها)
- [فصل ۸: انتقال ویژگی‌ها بین اشیاء](#فصل-۸-انتقال-ویژگی‌ها-بین-اشیاء)
- [فصل ۹: سازمان‌دهی داده‌ها](#فصل-۹-سازمان‌دهی-داده‌ها)
- [فصل ۱۰: ساده‌سازی منطق شرطی](#فصل-۱۰-ساده‌سازی-منطق-شرطی)
- [فصل ۱۱: بازآفرینی رابط برنامه‌نویسی](#فصل-۱۱-بازآفرینی-رابط-برنامه‌نویسی)
- [فصل ۱۲: مقابله با وراثت](#فصل-۱۲-مقابله-با-وراثت)

---

# پیش‌گفتار

> This book is about refactoring, specifically about refactoring in JavaScript, presented in a catalog format. Refactoring is a controlled technique for improving the design of an existing code base. Its essence is applying a series of small behavior-preserving transformations, each of which is "too small to be worth doing" on its own. By doing them in small steps you reduce the risk of introducing errors and get a system that is well tested at each step of the transformation.

این کتاب درباره بازآفرینی است، به‌طور خاص درباره بازآفرینی در جاوااسکریپت، ارائه‌شده به‌صورت فهرستی. بازآفرینی یک تکنیک کنترل‌شده برای بهبود طراحی یک پایگاه کد موجود است. ماهیت آن اعمال یک سری از تحولات کوچک حافظ رفتار است که هر یک به‌تنهایی «خیلی کوچک هستند که ارزش انجام داشته باشند». با انجام آن‌ها در گام‌های کوچک، خطر معرفی خطا را کاهش می‌دهید و سیستمی دریافت می‌کنید که در هر مرحله از تحول به‌خوبی آزمایش شده است.

> This book is aimed at two audiences. First, there's the software professional who's already familiar with JavaScript and probably with refactoring in other languages, and wants to learn about refactoring in JavaScript. Second is the developer who already knows refactoring from Fowler's original book, and wants to learn how to apply refactoring in JavaScript, particularly with the new features in ES6 and beyond.

این کتاب برای دو مخاطب نوشته شده است. اول، حرفه‌ای نرم‌افزاری که از قبل با جاوااسکریپت و احتمالاً با بازآفرینی در زبان‌های دیگر آشنا است و می‌خواهد درباره بازآفرینی در جاوااسکریپت بیاموزد. دوم، توسعه‌دهنده‌ای است که از قبل بازآفرینی را از کتاب اصلی فاولر می‌شناسد و می‌خواهد یاد بگیرد چگونه بازآفرینی را در جاوااسکریپت به کار ببندد، به‌ویژه با ویژگی‌های جدید ES6 و پس از آن.

---

# فصل ۱: بازآفرینی — چیستی و چرایی

⏱️ زمان مطالعه تقریبی: ۲۵ دقیقه

> Refactoring is the process of changing a software system in such a way that it does not alter the external behavior of the code yet improves its internal structure. It is a disciplined way to clean up code that minimizes the chances of introducing bugs. When you refactor software, you generally improve the design of existing code, make it easier to understand, and make it easier to maintain.

بازآفرینی فرآیند تغییر یک سیستم نرم‌افزاری به‌گونه‌ای است که رفتار بیرونی کد را تغییر ندهد اما ساختار درونی آن را بهبود بخشد. این یک روش منضبط برای پاکسازی کد است که احتمال معرفی باگ را به حداقل می‌رساند. هنگامی که نرم‌افزار را بازآفرینی می‌کنید، به‌طور کلی طراحی کد موجود را بهبود می‌بخشید، درک آن را آسان‌تر می‌کنید و نگهداری آن را ساده‌تر می‌سازید.

## چرا بازآفرینی می‌کنیم؟

> There are two additional reasons to refactor: understanding the software and preparing for a feature. The first reason, understanding, comes up whenever I need to change code. I find it hard to make changes to code that I don't understand well. With refactoring, I can improve my understanding of the code. It's a way of saying "I don't understand what's happening here. What does this code do?" and then doing something about it.

دو دلیل اضافی برای بازآفرینی وجود دارد: درک نرم‌افزار و آماده‌سازی برای یک ویژگی. دلیل اول، درک، هر زمانی که نیاز به تغییر کد دارم مطرح می‌شود. درک کدی که به‌خوبی نمی‌فهمم برایم سخت است. با بازآفرینی می‌توانم درکم از کد را بهبود بخشم.

## زمان بازآفرینی

> Don't try to refactor and add functionality at the same time. Make sure you have tests in place before you begin refactoring. The refactoring may change the external behavior, which could break a test. Take short steps and test frequently. Any change that you make to the code is a refactoring. It's a refactoring because it's a small change to the code; it preserves the behavior of the code.

سعی نکنید همزمان بازآفرینی کنید و ویژگی اضافه کنید. مطمئن شوید قبل از شروع بازآفرینی آزمایش‌هایی در جا دارید. بازآفرینی ممکن است رفتار بیرونی را تغییر دهد که می‌تواند یک آزمون را بشکند. گام‌های کوتاه بردارید و به‌طور مکرر آزمایش کنید.

## مشکلات کد بد

> I think of the following as the/7 signs that code needs refactoring:
> 1. Duplicated Code
> 2. Long Function
> 3. Large Class
> 4. Long Parameter List
> 5. Divergent Change
> 6. Shotgun Surgery
> 7. Feature Envy
> 8. Data Clumps
> 9. Primitive Obsession
> 10. Switch Statements
> 11. Parallel Inheritance Hierarchies
> 12. Lazy Class
> 13. Speculative Generality
> 14. Temporary Field
> 15. Message Chains
> 16. Middle Man
> 17. Insider Trading
> 18. Large Switch
> 19. Repetitive Associations

از نشانه‌های نیاز کد به بازآفرینی می‌توان به موارد زیر اشاره کرد: کد تکراری، تابع بلند، کلاس بزرگ، لیست پارامترهای بلند، تغییر واگرا، جراحی شاتگان، حسادت ویژگی، خوشه‌های داده، وسواس اولیه، عبارات سوئیچ، سلسله مراتب‌های وراثت موازی، کلاس تنبل، کلیت سودا، فیلد موقت، زنجیره‌های پیام، مرد میانی، تجارت داخلی، سوئیچ بزرگ و انجمن‌های تکراری.

## بازآفرینی و طراحی

> One of the most valuable things about refactoring is that it allows me to design less. I have always been a believer in design up front, and I still think that it's important to think through the design before you start building it. But design is never perfect. The best designs I know are those that evolve over time as the system is changed.

یکی از ارزشمندترین چیزها درباره بازآفرینی این است که به من اجازه می‌دهد کمتر طراحی کنم. طراحی هیچ‌وقت کامل نیست. بهترین طراحی‌هایی که می‌شناسم آن‌هایی هستند که در طول زمان همگام با تغییر سیستم تکامل می‌یابند.

---

# فصل ۲: نمونه‌ای از بازآفرینی

⏱️ زمان مطالعه تقریبی: ۴۵ دقیقه

> This chapter shows a progression of refactorings to a sample program. It starts with a fairly simple piece of code for calculating the amount to bill a theater for plays over a season. As we go through refactorings, we improve the code's clarity and add features.

این فصل یک پیشرفت از بازآفرینی‌ها را روی یک برنامه نمونه نشان می‌دهد. با یک قطعه کد نسبتاً ساده برای محاسبه مبلغ صورتحساب تئاتر برای نمایش‌ها در یک فصل شروع می‌شود. همان‌طور که بازآفرینی‌ها را انجام می‌دهیم، وضوح کد را بهبود می‌بخشیم و ویژگی‌ها اضافه می‌کنیم.

> We start with a function that calculates the amount a theater owes for plays over a season. The function takes a list of plays and a list of invoices, and returns a statement that shows the total amount owed. This example uses the structure of Statement Data, which is extracted from the raw data, and a renderPlainText function to produce a plain text version of the statement.

با تابعی شروع می‌کنیم که مبلغ بدهکاری تئاتر برای نمایش‌ها در یک فصل را محاسبه می‌کند. این تابع یک لیست از نمایش‌ها و یک لیست از صورتحساب‌ها می‌گیرد و بیانیه‌ای برمی‌گرداند که مبلغ کل بدهکاری را نشان می‌دهد.

> To begin the refactoring, I need to establish the solid bottom with tests. I'll start by creating tests based on the existing functionality. Then I can begin to refactor safely, running the tests after each change to ensure I haven't broken anything.

برای شروع بازآفرینی، باید پایه محکمی با آزمایش‌ها ایجاد کنم. با ایجاد آزمایش‌هایی بر اساس عملکرد موجود شروع می‌کنم. سپس می‌توانم با خیال راحت بازآفرینی را شروع کنم و بعد از هر تغییر آزمایش‌ها را اجرا کنم تا مطمئن شوم چیزی را نشکسته‌ام.

## استخراج تابع

> The first thing I do with a piece of code is figure out how to break it down. I look at the code and ask myself: "What is the intent of this code?" Then I try to extract the intent into a function with a name that says what it does.

اولین کاری که با یک قطعه کد انجام می‌دهم این است که بفهمم چگونه آن را تقسیم کنم. به کد نگاه می‌کنم و از خودم می‌پرسم: «قصد این کد چیست؟» سپس سعی می‌کنم قصد را در تابعی استخراج کنم که نامش بگوید چه کار می‌کند.

> I take a piece of code and name it to explain what it does. I extract the code into a function with that name. I then replace the old code with a call to the function. The key here is that the new function says what it does, rather than having to figure that out from the code itself.

یک قطعه کد برمی‌دارم و نامی به آن می‌دهم تا توضیح دهد چه کار می‌کند. کد را در تابعی با آن نام استخراج می‌کنم. سپس کد قدیمی را با فراخوانی تابع جایگزین می‌کنم. نکته کلیدی اینجاست که تابع جدید می‌گوید چه کار می‌کند، به جای اینکه لازم باشد از خود کد فهمید.

> Using Extract Function, I create a new function called renderPlainText. I move the code that does the actual rendering into this new function. Now I have a clear separation between the logic that creates the statement data and the logic that formats it for display.

با استفاده از استخراج تابع، تابع جدیدی به نام renderPlainText ایجاد می‌کنم. کدی که رندر واقعی را انجام می‌دهد به این تابع جدید منتقل می‌کنم. اکنون جداسازی واضحی بین منطقی که داده‌های بیانیه را ایجاد می‌کند و منطقی که آن را برای نمایش قالب‌بندی می‌کند، دارم.

## جایگزینی مقدار اولیه با شیء

> When I see data structures where several fields are always passed together, I consider replacing them with an object. This can simplify function signatures and make the code more expressive. It also makes it easier to add new behavior related to that data structure.

وقتی ساختارهای داده‌ای می‌بینم که چند فیلد همیشه با هم پاس داده می‌شوند، جایگزینی آن‌ها با یک شیء را در نظر می‌گیرم. این می‌تواند امضای تابع را ساده کند و کد را بیانگرتر سازد.

## تقسیم حلقه

> I can split the statement into two parts: one to compute the data and one to render it. This separation means I can reuse the computation of the data in different ways—by rendering it in HTML, for instance. This is a common pattern: separate the computation from the presentation.

می‌توانم بیانیه را به دو بخش تقسیم کنم: یکی برای محاسبه داده‌ها و دیگری برای رندر کردن آن. این جداسازی به این معنی است که می‌توانم محاسبه داده‌ها را به شیوه‌های مختلف بازاستفاده کنم—مثلاً با رندر کردن آن در HTML.

## استخراج کلاس صورتحساب

> When I have data and functions that operate on them together, I often end up with a class. The statement function creates the data structure and the render functions operate on it. I extract a Statement class from this, encapsulating the data and the rendering together. This encapsulation makes the code much easier to work with, because I can now clearly see what operations are available on the statement data.

وقتی داده‌ها و توابعی دارم که با هم عمل می‌کنند، اغلب به یک کلاس ختم می‌شوم. تابع statement ساختار داده را ایجاد می‌کند و توابع render روی آن عمل می‌کنند. یک کلاس Statement از این‌ها استخراج می‌کنم و داده‌ها و رندرینگ را با هم محصور می‌کنم.

## استخراج تابع محاسبه هزینه

> I extract the computation of the charge into its own function. This separates the calculation from the formatting, making both easier to understand and modify independently. The charge function takes a performance and returns a number.

محاسبه هزینه را در تابع مستقل خودش استخراج می‌کنم. این محاسبه را از قالب‌بندی جدا می‌کند و هر دو را آسان‌تر می‌سازد.

## جایگزینی متد با تابع

> Sometimes I find that a function in one class really belongs in another class. When that happens, I use Move Function to put it where it belongs. Or I might find that a method is more naturally expressed as a standalone function.

گاهی اوقات متوجه می‌شوم که تابعی در یک کلاس واقعاً در کلاس دیگری قرار دارد. وقتی این اتفاق می‌افتد، از Move Function استفاده می‌کنم تا آن را به جای خودش ببرم.

## تبدیل شرطی به پلیمورفیسم

> This is one of the more important refactorings in the book. I have a function that uses a conditional to select among several behaviors. I replace the conditional with polymorphism, using subclasses or strategy pattern to handle the different cases. This eliminates the conditional logic and makes the code more extensible.

این یکی از مهم‌ترین بازآفرینی‌های کتاب است. تابعی دارم که از شرطی برای انتخاب بین رفتارهای مختلف استفاده می‌کند. شرطی را با پلیمورفیسم جایگزین می‌کنم.

## استخراج زیرکلاس

> After applying Replace Type Code with Subclasses, I might find that subclasses have different behavior. I extract common behavior into a superclass and let the subclasses provide the variations. This is how inheritance hierarchies evolve.

پس از اعمال جایگزینی کد نوع با زیرکلاس‌ها، ممکن است متوجه شوم زیرکلاس‌ها رفتار متفاوتی دارند.

---

# فصل ۳: فرهنگ بازآفرینی

⏱️ زمان مطالعه تقریبی: ۲۰ دقیقه

> Refactoring is a powerful tool, but like all tools, it's not a silver bullet. To use it effectively, you need to develop a good sense of how to do it, and to build a culture where refactoring is part of everyday development. The best way to learn refactoring is to have someone experienced guide you through it.

بازآفرینی ابزار قدرتمندی است، اما مانند تمام ابزارها، یک گلوله نقره‌ای نیست. برای استفاده مؤثر از آن، باید حس خوبی از نحوه انجام آن پرورش دهید و فرهنگی بسازید که بازآفرینی بخشی از توسعه روزمره باشد.

## تعداد بازآفرینی‌های اضافه‌شده

> Some refactorings in this book are expanded in coverage from the first edition, and I've added several new ones. Not all of these are major refactorings. Some are simple helper techniques that I've found useful. The catalog is intended to be used as a reference; you don't need to read it from cover to cover.

برخی از بازآفرینی‌های این کتاب نسبت به ویرایش اول گسترش یافته‌اند و چندین مورد جدید اضافه کرده‌ام. کاتالوگ به‌عنوان مرجع در نظر گرفته شده است؛ لازم نیست آن را از اول تا آخر بخوانید.

## قوانین بازآفرینی

> The Rule of Refactoring: When you do refactoring, you should always have a refactoring to do. The first is that the process of refactoring is closely tied to testing. A refactoring change is a very small one; you should test after every such change. If I'm working on a large refactoring and realize I need to make a small change that's not a refactoring, I make that small change, test, then continue with the refactoring.

قانون بازآفرینی: وقتی بازآفرینی می‌کنید، همیشه باید بازآفرینی‌ای برای انجام داشته باشید. فرآیند بازآفرینی با آزمایش کردن پیوند تنگاتنگی دارد. هر تغییر بازآفرینی بسیار کوچک است و باید بعد از هر تغییر آزمایش کنید.

## ارتباط با کلیات (High Level)

> One way I think about refactoring is that it's like work you do on the foundation of a house. You don't change the visible appearance (the facade), but you strengthen the foundation so that you can add new rooms more easily. When you have a strong foundation, you can extend the house in many directions.

یکی از راه‌های فکر کردن درباره بازآفرینی این است که مانند کاری است که روی فونداسیون خانه انجام می‌دهید. ظاهر قابل مشاهده (نمای بیرونی) را تغییر نمی‌دهید، اما فونداسیون را تقویت می‌کنید تا بتوانید اتاق‌های جدید را راحت‌تر اضافه کنید.

---

# فصل ۴: شروع کار

⏱️ زمان مطالعه تقریبی: ۱۵ دقیقه

> To start refactoring, you have to do it from a base of understanding. The first step is to look at the code and understand what it does. You need a test suite that checks the code's behavior. Once you have that understanding, you can start to make small, behavior-preserving changes to the code.

برای شروع بازآفرینی، باید از پایه درک شروع کنید. اولین قدم نگاه کردن به کد و فهمیدن این است که چه کار می‌کند. به مجموعه آزمایش‌هایی نیاز دارید که رفتار کد را بررسی کند.

## آزمون‌ها

> If I want to refactor carefully, I must have a suite of tests that I can run quickly and verify that my refactoring has not broken anything. It's important that these tests are self-checking. A test suite is the best safety net when refactoring; without tests, refactoring is a slow and risky process.

اگر می‌خواهم با دقت بازآفرینی کنم، باید مجموعه آزمایش‌هایی داشته باشم که بتوانم به‌سرعت اجرا کنم و بررسی کنم که بازآفرینی‌ام چیزی را نشکسته است. بدون آزمایش‌ها، بازآفرینی فرآیندی کند و پرخطر است.

## یافتن نقطه شروع

> When you're looking to refactor, you're usually looking at a large piece of code. You don't want to try to refactor the entire program at once. Instead, find a small part that you can refactor in isolation. Start with a function that's hard to understand, or a class that's doing too much.

وقتی دنبال بازآفرینی می‌گردید، معمولاً به یک قطعه کد بزرگ نگاه می‌کنید. نمی‌خواهید کل برنامه را یکجا بازآفرینی کنید. در عوض، بخش کوچکی پیدا کنید که بتوانید آن را به‌صورت جداگانه بازآفرینی کنید.

---

# فصل ۵: هوشمندتر عمل کردن

⏱️ زمان مطالعه تقریبی: ۳۰ دقیقه

> Once you've learned the basic refactorings, you'll want to move beyond the individual refactoring techniques. This chapter provides guidance on how to combine refactorings to accomplish more complex changes. The key is to work in small steps, using refactoring techniques to build up to the larger change you want to make.

وقتی بازآفرینی‌های پایه‌ای را یاد گرفتید، می‌خواهید فراتر از تکنیک‌های فردی بازآفرینی حرکت کنید. این فصل راهنمایی درباره نحوه ترکیب بازآفرینی‌ها برای انجام تغییرات پیچیده‌تر ارائه می‌دهد.

## ترکیب بازآفرینی‌ها

> To do refactoring well, you need to build up a habit of combining small refactorings into larger ones. Each individual refactoring is a small step, but they add up to significant improvements in the design of your code.

برای بازآفرینی خوب، باید عادت ترکیب بازآفرینی‌های کوچک به بازآفرینی‌های بزرگ‌تر را پرورش دهید. هر بازآفرینی فردی یک قدم کوچک است، اما مجموع آن‌ها به بهبودهای قابل‌توجهی در طراحی کد شما منجر می‌شود.

## ریشه‌یابی مشکلات

> Often when I see code that needs refactoring, I start with a surface problem (the code is hard to understand) and then find that the real issue is deeper (the abstraction is wrong). As I refactor, I fix surface issues first, which reveals deeper problems that I can then address.

اغلب وقتی کدی می‌بینم که به بازآفرینی نیاز دارد، با یک مشکل سطحی شروع می‌کنم (کد سخت قابل فهم است) و سپس متوجه می‌شوم مشکل واقعی عمیق‌تر است (ابعاد اشتباه است).

---

# فصل ۶: مجموعه اول بازآفرینی‌ها

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

# فصل ۷: محصورسازی داده‌ها

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

# فصل ۸: انتقال ویژگی‌ها بین اشیاء

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

# فصل ۹: سازمان‌دهی داده‌ها

⏱️ زمان مطالعه تقریبی: ۳۰ دقیقه

> This chapter covers techniques for better organizing data within your code. Good data organization is critical for keeping code maintainable. These techniques help you avoid problems like dangling references and ensure your data stays consistent.

این فصل تکنیک‌هایی برای سازمان‌دهی بهتر داده‌ها در کد شما را پوشش می‌دهد.

---

### 21. جدا کردن متغیر — Split Variable

> When I have a variable that is used for two different things, I split it into two separate variables. If a variable is assigned to twice, and each assignment has a different reason for existing, I create two separate variables. This makes each variable's purpose clearer.

وقتی متغیری دارم که برای دو چیز مختلف استفاده می‌شود، آن را به دو متغیر جداگانه تقسیم می‌کنم.

---

### 22. تغییر مرجع به مقدار — Change Reference to Value

> Replaces a reference to an object with a value object. If I have a class that references another object, but the reference is never used to distinguish identity, I can convert it to a value—copying the data instead of referencing it. This simplifies the code.

مرجع به یک شیء را با یک شیء مقداری جایگزین می‌کند.

---

### 23. تغییر مقدار به مرجع — Change Value to Reference

> Replaces a value with a reference. When I have several objects that have the same data and I need to treat them as a single object, I convert the value to a reference. This is the opposite of Change Reference to Value.

یک مقدار را با یک مرجع جایگزین می‌کند. وقتی چند شیء دارم که داده یکسانی دارند و باید آن‌ها را به‌عنوان یک شیء واحد در نظر بگیرم.

---

### 24. جایگزینی متغیر مشتق با پرس و جو — Replace Derived Variable with Query

> Replaces a variable that's calculated from other data with a function that calculates it each time. If I have a field that's derived from other fields, and it's kept in sync with them manually, I replace it with a query method that computes it on the fly. This eliminates the risk of the derived data getting out of sync.

متغیری که از سایر داده‌ها محاسبه شده با تابعی جایگزین می‌کند که هر بار آن را محاسبه می‌کند.

---

# فصل ۱۰: ساده‌سازی منطق شرطی

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

# فصل ۱۱: بازآفرینی رابط برنامه‌نویسی

⏱️ زمان مطالعه تقریبی: ۵۰ دقیقه

> APIs are the hardest part of a library to change once it's in widespread use. This chapter covers techniques for working with APIs, making them easier to use and evolve. The key insight is that a well-designed API makes refactoring the implementation easier.

رابط‌های برنامه‌نویسی سخت‌ترین بخش یک کتابخانه برای تغییر پس از استفاده گسترده هستند.

---

### 32. جدا کردن جستجو از تغییردهنده — Separate Query from Modifier

> Separates a method that returns a value from one that has a side effect. A function should either answer a question or modify the state of the system—but not both. This is the Command-Query Separation principle. When I find a method that both returns a value and has a side effect, I split it into two methods.

متدی که مقداری برمی‌گرداند را از متدی که اثر جانبی دارد جدا می‌کند. تابع باید یا سؤالی پاسخ دهد یا وضعیت سیستم را تغییر دهد—نه هر دو.

---

### 33. پارامتری کردن تابع — Parameterize Function

> Takes a piece of code that does similar things in slightly different ways and adjusts it to take additional parameters that allow it to be used more widely. Instead of having several functions that differ only in their literal values, I create one function that takes those values as parameters.

یک قطعه کد که کارهای مشابهی را به شیوه‌های کمی متفاوت انجام می‌دهد برمی‌دارد و آن را طوری تنظیم می‌کند که پارامترهای اضافی بگیرد.

---

### 34. حذف پارامتر — Remove Parameter

> Removes a parameter from a function. If a function's parameter is no longer used, I remove it. This simplifies the function's interface. It's a simple refactoring, but I need to make sure no callers are passing that parameter anymore.

یک پارامتر را از تابع حذف می‌کند.

---

### 35. حفظ کل شیء — Preserve Whole Object

> Takes a value from an object and passes it as a parameter instead. This is the inverse of Replace Parameter with Query. Instead of extracting a value from an object to pass to a function, I pass the whole object. This reduces the number of parameters and makes the code more robust to changes.

مقداری را از یک شیء برمی‌دارد و آن را به‌جای آن به‌عنوان پارامتر پاس می‌دهد.

---

### 36. جایگزینی پارامتر با پرس و جو — Replace Parameter with Query

> Replaces a parameter with a query that gets the value. If a function always uses the same value for one of its parameters, I can remove the parameter and call the function that provides that value instead. This simplifies the caller's job.

یک پارامتر را با پرس و جویی که مقدار را دریافت می‌کند جایگزین می‌کند.

---

### 37. جایگزینی پارامتر با مقادیر صریح — Replace Parameter with Explicit Values

> Replaces a parameter with an explicit value. If a function always gets the same value for one of its parameters, I replace the parameter with that value. This makes the call clearer. This is the opposite of Parameterize Function.

یک پارامتر را با مقدار صریح جایگزین می‌کند.

---

### 38. حذف متد تنظیم — Remove Setting Method

> Removes a setting method that shouldn't exist. If a field shouldn't be changed after an object is created, I remove the setter method. For fields that need to be set during construction, I move them to the constructor. This makes the intent clearer—the field is immutable after creation.

متد تنظیمی را حذف می‌کند که نباید وجود داشته باشد. اگر فیلدی نباید پس از ایجاد شیء تغییر کند، متد setter را حذف می‌کنم.

---

### 39. جایگزینی سازنده با تابع کارخانه‌ای — Replace Constructor with Factory Function

> Replaces a constructor call with a factory function. Factory functions are more flexible than constructors—they can return different subtypes, use descriptive names, and don't require the "new" keyword. In JavaScript, factory functions are a common and idiomatic pattern.

فراخوانی سازنده را با تابع کارخانه‌ای جایگزین می‌کند. توابع کارخانه‌ای انعطاف‌پذیرتر از سازنده‌ها هستند—می‌توانند زیرنوع‌های مختلف برگردانند، نام‌های توصیفی استفاده کنند و به کلمه کلیدی "new" نیاز ندارند.

---

### 40. جایگزینی تابع با فرمان — Replace Function with Command

> Turns a function into its own command object. When a function is complex and I need to manipulate its parameters over time, build up its state, or support undo, I turn it into a command object. The command object has an execute method that does the same thing the function did.

تابع را به شیء فرمان خودش تبدیل می‌کند. وقتی تابع پیچیده است و باید پارامترهایش را در طول زمان دستکاری کنم.

---

### 41. جایگزینی فرمان با تابع — Replace Command with Function

> Replaces a command object with a function. This is the inverse of Replace Function with Command. If a command object is simple and I don't need its extra features (like undo, parameter building, etc.), I turn it back into a plain function.

شیء فرمان را با تابع جایگزین می‌کند. این معکوس جایگزینی تابع با فرمان است.

---

# فصل ۱۲: مقابله با وراثت

⏱️ زمان مطالعه تقریبی: ۶۰ دقیقه

> Inheritance is one of the most well-known features of object-oriented programming. Like any powerful mechanism, it is both very useful and easy to misuse. It's often hard to see the misuse until it's in the rear-view mirror. This chapter covers techniques for working with inheritance hierarchies—moving features up and down the hierarchy, adding and removing classes, and converting inheritance to delegation when it's no longer appropriate.

وراثت یکی از شناخته‌شده‌ترین ویژگی‌های برنامه‌نویسی شیءگرا است. مانند هر مکانیزم قدرتمندی، هم بسیار مفید و هم مستعد سوءاستفاده است.

---

### 42. کشیدن متد به بالا — Pull Up Method

> Moves a method from a subclass into its superclass. This is one of the most common inheritance-related refactorings. When two subclasses have duplicate methods, I move one into the superclass. The key is to ensure that both methods do the same thing before pulling one up. If they differ slightly, I first use Parameterize Function to unify them.

متدی را از یک زیرکلاس به کلاس والد آن منتقل می‌کند. این یکی از رایج‌ترین بازآفرینی‌های مرتبط با وراثت است. وقتی دو زیرکلاس متدهای تکراری دارند، یکی را به کلاس والد منتقل می‌کنم.

---

### 43. کشیدن فیلد به بالا — Pull Up Field

> Moves a field from a subclass to its superclass. When two subclasses have fields with the same meaning (even if named differently), I move one to the superclass. This reduces duplication in the data structure. In dynamic languages, pulling up a field is essentially a consequence of Pull Up Constructor Body.

فیلدی را از زیرکلاس به کلاس والد منتقل می‌کند. وقتی دو زیرکلاس فیلدهایی با معنای یکسان دارند.

---

### 44. کشیدن بدنه سازنده به بالا — Pull Up Constructor Body

> Moves common statements in subclass constructors to the superclass constructor. If I see duplicate code in constructor bodies of subclasses, I extract the common code and put it in the superclass constructor using a super() call.

دستورات مشترک در سازنده‌های زیرکلاس‌ها را به سازنده کلاس والد منتقل می‌کند.

---

### 45. هل دادن متد به پایین — Push Down Method

> Moves a method from a superclass into its subclass. If a method is only relevant to one subclass, it should live in that subclass. This is the inverse of Pull Up Method. This refactoring makes it clear that the method is specialized for a particular subclass.

متدی را از کلاس والد به زیرکلاس آن منتقل می‌کند. اگر متد فقط برای یک زیرکلاس مرتبط است، باید در آن زیرکلاس باشد.

---

### 46. هل دادن فیلد به پایین — Push Down Field

> Moves a field from a superclass to its subclass. If a field is only used by one subclass, it should live in that subclass. This is the inverse of Pull Up Field.

فیلدی را از کلاس والد به زیرکلاس آن منتقل می‌کند.

---

### 47. جایگزینی کد نوع با زیرکلاس‌ها — Replace Type Code with Subclasses

> Replaces a type code field with subclasses. Instead of using a field to indicate the type of an object, I create a subclass for each type. Each subclass overrides behavior that differs by type. I use a factory function to decide which subclass to create based on the type code.

یک فیلد کد نوع را با زیرکلاس‌ها جایگزین می‌کند. به جای استفاده از فیلد برای نشان دادن نوع یک شیء، برای هر نوع زیرکلاسی ایجاد می‌کنم.

---

### 48. حذف زیرکلاس — Remove Subclass

> Replaces a subclass with a field in the superclass. Sometimes subclasses become too small and aren't worth the complexity they add. When a subclass doesn't add enough behavior to justify its existence, I remove it and represent the variation with a field instead.

زیرکلاس را با فیلدی در کلاس والد جایگزین می‌کند. گاهی زیرکلاس‌ها خیلی کوچک می‌شوند و ارزش پیچیدگی‌ای که اضافه می‌کنند را ندارند.

---

### 49. استخراج کلاس والد — Extract Superclass

> Creates a superclass from two classes with similar features. When two classes have common fields and methods, I create a superclass and move the common elements to it using Pull Up Field and Pull Up Method. This is the inheritance alternative to Extract Class.

کلاس والدی را از دو کلاس با ویژگی‌های مشابه ایجاد می‌کند. وقتی دو کلاس فیلدها و متدهای مشترک دارند.

---

### 50. فروپاشی سلسله مراتب — Collapse Hierarchy

> Merges a superclass and one of its subclasses into a single class. When a class and its parent are no longer different enough to be worth keeping separate, I merge them together. I choose which one to keep based on which name makes the most sense for the future.

کلاس والد و یکی از زیرکلاس‌هایش را در یک کلاس واحد ادغام می‌کند.

---

### 51. جایگزینی زیرکلاس با نماینده — Replace Subclass with Delegate

> Replaces inheritance with delegation. This is used when a subclass is used for more than just polymorphic behavior—when I want to change the type at runtime, or when I have more than one reason to vary the behavior. Instead of inheritance, I create a delegate class and have the superclass delegate to it.

وراثت را با نمایندگی جایگزین می‌کند. این زمانی استفاده می‌شود که زیرکلاس بیش از رفتار پلیمورفیک استفاده می‌شود—وقتی می‌خواهم نوع را در زمان اجرا تغییر دهم یا بیش از یک دلیل برای تغییر رفتار دارم.

> There is a popular principle: "Favor object composition over class inheritance." This doesn't mean we should never use inheritance. Inheritance is a valuable mechanism that does the job most of the time. So I reach for it first, and move onto delegation when it starts to become a problem.

اصول محبوبی وجود دارد: «ترجیح ترکیب اشیاء بر وراثت کلاس‌ها». این به این معنی نیست که هرگز نباید از وراثت استفاده کنیم. وراثت مکانیزم ارزشمندی است که بیشتر اوقات کار می‌کند.

---

### 52. جایگزینی کلاس والد با نماینده — Replace Superclass with Delegate

> Replaces inheritance with delegation to a separate object. This is used when the superclass functions don't make sense on the subclass, or when the subclass should not be an instance of the superclass in all cases. For example, making a stack a subclass of list is wrong because not all list operations apply to a stack.

وراثت را با نمایندگی به یک شیء جداگانه جایگزین می‌کند. این زمانی استفاده می‌شود که توابع کلاس والد در زیرکلاس معنا ندارند.

> Even in cases where the subclass is a reasonable modeling, I use Replace Superclass with Delegate because the relationship between a subclass and a superclass is highly coupled, with the subclass easily broken by changes in the superclass. The downside is that I need to write forwarding functions, but fortunately, these are too simple to get wrong.

حتی در مواردی که زیرکلاس مدل‌سازی معقولی است، از جایگزینی کلاس والد با نماینده استفاده می‌کنم زیرا رابطه بین زیرکلاس و کلاس والد بسیار محکم است و زیرکلاس به‌راحتی با تغییرات کلاس والد شکسته می‌شود.

---

# خلاصه فصل ۱۲

وراثت ابزار قدرتمندی است اما باید با احتیاط استفاده شود. کشیدن به بالا و هل دادن به پایین به شما امکان می‌دهند ویژگی‌ها را در سلسله مراتب حرکت دهید. استخراج کلاس والد و فروپاشی سلسله مراتب به شما امکان ساختاربندی مجدد سلسله مراتب را می‌دهند. و جایگزینی با نماینده وقتی استفاده می‌شود که وراثت دیگر بهترین انتخاب نباشد.

---

# پایان کتاب

> This book has covered the major refactorings I've found useful over the years, with examples in JavaScript. The catalog is meant to be used as a reference—each entry describes a specific refactoring with its motivation, mechanics, and examples. When you encounter code smells in your work, refer to the catalog for guidance on how to refactor.

این کتاب بازآفرینی‌های اصلی‌ای را که در طول سال‌ها مفید یافته‌ام، با مثال‌هایی در جاوااسکریپت، پوشش داده است. کاتالوگ به‌عنوان مرجع طراحی شده—هر مدخل یک بازآفرینی خاص را با انگیزه، مکانیک‌ها و مثال‌هایش توصیف می‌کند.

---

*ترجمه کتاب بازآفرینی کد — مارتین فاولر (ویرایش دوم)*  
*تمامی مثال‌های کد به زبان اصلی (جاوااسکریپت) حفظ شده‌اند.*
