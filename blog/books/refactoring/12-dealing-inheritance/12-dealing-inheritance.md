> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۳۲۳

> Inheritance is one of the most well-known features of object-oriented programming. Like any powerful mechanism, it is both very useful and easy to misuse. It's often hard to see the misuse until it's in the rear-view mirror. This chapter covers techniques for working with inheritance hierarchies—moving features up and down the hierarchy, adding and removing classes, and converting inheritance to delegation when it's no longer appropriate.

وراثت یکی از شناخته‌شده‌ترین ویژگی‌های برنامه‌نویسی شیءگرا است. مانند هر مکانیزم قدرتمندی، هم بسیار مفید و هم مستعد سوءاستفاده است.

![Section](images/page001-323.png)

![Section](images/page002-324.png)

![Section](images/page003-325.png)

![Section](images/page004-326.png)

![Section](images/page005-327.png)

![Section](images/page006-328.png)

![Section](images/page007-329.png)

![Section](images/page008-330.png)

---

###### 📄 صفحه ۳۳۱

> Moves a method from a subclass into its superclass. This is one of the most common inheritance-related refactorings. When two subclasses have duplicate methods, I move one into the superclass. The key is to ensure that both methods do the same thing before pulling one up. If they differ slightly, I first use Parameterize Function to unify them.

متدی را از یک زیرکلاس به کلاس والد آن منتقل می‌کند. این یکی از رایج‌ترین بازآفرینی‌های مرتبط با وراثت است. وقتی دو زیرکلاس متدهای تکراری دارند، یکی را به کلاس والد منتقل می‌کنم.

![Section](images/page009-331.png)

![Section](images/page010-332.png)

![Section](images/page011-333.png)

![Section](images/page012-334.png)

![Section](images/page013-335.png)

![Section](images/page014-336.png)

![Section](images/page015-337.png)

![Section](images/page016-338-img1.png)

---

###### 📄 صفحه ۳۳۹

> Moves a field from a subclass to its superclass. When two subclasses have fields with the same meaning (even if named differently), I move one to the superclass. This reduces duplication in the data structure. In dynamic languages, pulling up a field is essentially a consequence of Pull Up Constructor Body.

فیلدی را از زیرکلاس به کلاس والد منتقل می‌کند. وقتی دو زیرکلاس فیلدهایی با معنای یکسان دارند.

![Section](images/page017-339.png)

![Section](images/page018-340.png)

![Section](images/page019-341.png)

![Section](images/page020-342.png)

![Section](images/page021-343-img1.png)

![Section](images/page022-344.png)

![Section](images/page023-345.png)

![Section](images/page024-346.png)

---

###### 📄 صفحه ۳۴۷

> Moves common statements in subclass constructors to the superclass constructor. If I see duplicate code in constructor bodies of subclasses, I extract the common code and put it in the superclass constructor using a super() call.

دستورات مشترک در سازنده‌های زیرکلاس‌ها را به سازنده کلاس والد منتقل می‌کند.

![Section](images/page025-347-img1.png)

![Section](images/page026-348.png)

![Section](images/page027-349.png)

![Section](images/page028-350.png)

![Section](images/page029-351-img1.png)

![Section](images/page030-352.png)

![Section](images/page031-353.png)

![Section](images/page032-354.png)

---

###### 📄 صفحه ۳۵۵

> Moves a method from a superclass into its subclass. If a method is only relevant to one subclass, it should live in that subclass. This is the inverse of Pull Up Method. This refactoring makes it clear that the method is specialized for a particular subclass.

متدی را از کلاس والد به زیرکلاس آن منتقل می‌کند. اگر متد فقط برای یک زیرکلاس مرتبط است، باید در آن زیرکلاس باشد.

![Section](images/page033-355.png)

![Section](images/page034-356-img1.png)

![Section](images/page035-357.png)

![Section](images/page036-358.png)

![Section](images/page037-359.png)

![Section](images/page038-360.png)

![Section](images/page039-361.png)

![Section](images/page040-362.png)

---

###### 📄 صفحه ۳۶۳

> Moves a field from a superclass to its subclass. If a field is only used by one subclass, it should live in that subclass. This is the inverse of Pull Up Field.

فیلدی را از کلاس والد به زیرکلاس آن منتقل می‌کند.

![Section](images/page041-363-img1.png)

![Section](images/page042-364.png)

![Section](images/page043-365.png)

![Section](images/page044-366-img1.png)

![Section](images/page045-367.png)

![Section](images/page046-368.png)

![Section](images/page047-369.png)

![Section](images/page048-370.png)

---

###### 📄 صفحه ۳۷۱

> Replaces a type code field with subclasses. Instead of using a field to indicate the type of an object, I create a subclass for each type. Each subclass overrides behavior that differs by type. I use a factory function to decide which subclass to create based on the type code.

یک فیلد کد نوع را با زیرکلاس‌ها جایگزین می‌کند. به جای استفاده از فیلد برای نشان دادن نوع یک شیء، برای هر نوع زیرکلاسی ایجاد می‌کنم.

![Section](images/page049-371-img1.png)

![Section](images/page050-372.png)

![Section](images/page051-373-img1.png)

![Section](images/page052-374.png)

![Section](images/page053-375.png)

![Section](images/page054-376.png)

![Section](images/page055-377-img1.png)

![Section](images/page056-378.png)

---

###### 📄 صفحه ۳۷۹

> Replaces a subclass with a field in the superclass. Sometimes subclasses become too small and aren't worth the complexity they add. When a subclass doesn't add enough behavior to justify its existence, I remove it and represent the variation with a field instead.

زیرکلاس را با فیلدی در کلاس والد جایگزین می‌کند. گاهی زیرکلاس‌ها خیلی کوچک می‌شوند و ارزش پیچیدگی‌ای که اضافه می‌کنند را ندارند.

![Section](images/page057-379.png)

![Section](images/page058-380.png)

![Section](images/page059-381.png)

![Section](images/page060-382.png)

![Section](images/page061-383.png)

![Section](images/page062-384-img1.png)

![Section](images/page063-385.png)

![Section](images/page064-386.png)

---

###### 📄 صفحه ۳۸۷

> Creates a superclass from two classes with similar features. When two classes have common fields and methods, I create a superclass and move the common elements to it using Pull Up Field and Pull Up Method. This is the inheritance alternative to Extract Class.

کلاس والدی را از دو کلاس با ویژگی‌های مشابه ایجاد می‌کند. وقتی دو کلاس فیلدها و متدهای مشترک دارند.

![Section](images/page065-387.png)

![Section](images/page066-388.png)

![Section](images/page067-389.png)

![Section](images/page068-390-img1.png)

![Section](images/page069-391.png)

![Section](images/page070-392.png)

![Section](images/page071-393-img1.png)

![Section](images/page072-394.png)

---

###### 📄 صفحه ۳۹۵

> Merges a superclass and one of its subclasses into a single class. When a class and its parent are no longer different enough to be worth keeping separate, I merge them together. I choose which one to keep based on which name makes the most sense for the future.

کلاس والد و یکی از زیرکلاس‌هایش را در یک کلاس واحد ادغام می‌کند.

![Section](images/page073-395-img1.png)

![Section](images/page074-396.png)

![Section](images/page075-397.png)

![Section](images/page076-398.png)

![Section](images/page077-399-img1.png)

![Section](images/page078-400-img1.png)

![Section](images/page079-401-img1.png)

![Section](images/page080-402.png)

---

###### 📄 صفحه ۴۰۳

> Replaces inheritance with delegation. This is used when a subclass is used for more than just polymorphic behavior—when I want to change the type at runtime, or when I have more than one reason to vary the behavior. Instead of inheritance, I create a delegate class and have the superclass delegate to it.

وراثت را با نمایندگی جایگزین می‌کند. این زمانی استفاده می‌شود که زیرکلاس بیش از رفتار پلیمورفیک استفاده می‌شود—وقتی می‌خواهم نوع را در زمان اجرا تغییر دهم یا بیش از یک دلیل برای تغییر رفتار دارم.

![Section](images/page081-403.png)

![Section](images/page082-404.png)

![Section](images/page083-405.png)

![Section](images/page084-406.png)

![Section](images/page085-407.png)

![Section](images/page086-408.png)

![Section](images/page087-409.png)

![Section](images/page088-410-img1.png)

---

###### 📄 صفحه ۴۱۱

> There is a popular principle: "Favor object composition over class inheritance." This doesn't mean we should never use inheritance. Inheritance is a valuable mechanism that does the job most of the time. So I reach for it first, and move onto delegation when it starts to become a problem.

اصول محبوبی وجود دارد: «ترجیح ترکیب اشیاء بر وراثت کلاس‌ها». این به این معنی نیست که هرگز نباید از وراثت استفاده کنیم. وراثت مکانیزم ارزشمندی است که بیشتر اوقات کار می‌کند.

![Section](images/page089-411.png)

![Section](images/page090-412.png)

![Section](images/page091-413.png)

![Section](images/page092-414.png)

![Section](images/page093-415.png)

![Section](images/page094-416.png)

![Section](images/page095-417-img1.png)

![Section](images/page096-418.png)

---

###### 📄 صفحه ۴۱۹

> Replaces inheritance with delegation to a separate object. This is used when the superclass functions don't make sense on the subclass, or when the subclass should not be an instance of the superclass in all cases. For example, making a stack a subclass of list is wrong because not all list operations apply to a stack.

وراثت را با نمایندگی به یک شیء جداگانه جایگزین می‌کند. این زمانی استفاده می‌شود که توابع کلاس والد در زیرکلاس معنا ندارند.

![Section](images/page097-419.png)

![Section](images/page098-420.png)

![Section](images/page099-421.png)

![Section](images/page100-422.png)

![Section](images/page101-423-img1.png)

![Section](images/page102-424-img1.png)

![Section](images/page103-425.png)

![Section](images/page104-426.png)

---

###### 📄 صفحه ۴۲۷

> Even in cases where the subclass is a reasonable modeling, I use Replace Superclass with Delegate because the relationship between a subclass and a superclass is highly coupled, with the subclass easily broken by changes in the superclass. The downside is that I need to write forwarding functions, but fortunately, these are too simple to get wrong.

حتی در مواردی که زیرکلاس مدل‌سازی معقولی است، از جایگزینی کلاس والد با نماینده استفاده می‌کنم زیرا رابطه بین زیرکلاس و کلاس والد بسیار محکم است و زیرکلاس به‌راحتی با تغییرات کلاس والد شکسته می‌شود.

![Section](images/page105-427.png)

![Section](images/page106-428.png)

![Section](images/page107-429.png)

![Section](images/page108-430.png)

![Section](images/page109-431.png)

![Section](images/page110-432.png)

![Section](images/page111-433.png)

![Section](images/page112-434.png)

---

###### 📄 صفحه ۴۳۵

> This book has covered the major refactorings I've found useful over the years, with examples in JavaScript. The catalog is meant to be used as a reference—each entry describes a specific refactoring with its motivation, mechanics, and examples. When you encounter code smells in your work, refer to the catalog for guidance on how to refactor.

این کتاب بازآفرینی‌های اصلی‌ای را که در طول سال‌ها مفید یافته‌ام، با مثال‌هایی در جاوااسکریپت، پوشش داده است. کاتالوگ به‌عنوان مرجع طراحی شده—هر مدخل یک بازآفرینی خاص را با انگیزه، مکانیک‌ها و مثال‌هایش توصیف می‌کند.

![Section](images/page113-435.png)

![Section](images/page114-436.png)

![Section](images/page115-437.png)

![Section](images/page116-438.png)

![Section](images/page117-439.png)

![Section](images/page118-440.png)

![Section](images/page119-441.png)

![Section](images/page120-442.png)

![Section](images/page121-443.png)

![Section](images/page122-444.png)

![Section](images/page123-445.png)

![Section](images/page124-446.png)

![Section](images/page125-447-img1.png)

![Section](images/page126-448.png)

![Section](images/page127-449.png)

![Section](images/page128-450.png)

![Section](images/page129-451.png)

![Section](images/page130-452.png)

![Section](images/page131-453.png)

![Section](images/page132-454-img1.jpeg)

![Section](images/page133-455-img1.jpeg)

---
