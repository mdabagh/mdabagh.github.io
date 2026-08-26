## ۲۸. جداسازی (Decoupling)



![Bend, or Break](images/page001-171.png)

![Bend, or Break](images/page009-179-img26.png)

![Bend, or Break](images/page027-197.png)

![Bend, or Break](images/page036-206-img116.png)

![Bend, or Break](images/page036-206-img141.png)

![Bend, or Break](images/page036-206-img167.png)

![Bend, or Break](images/page036-206-img192.png)

![Bend, or Break](images/page036-206-img217.png)

![Bend, or Break](images/page036-206-img242.png)

![Bend, or Break](images/page036-206-img268.png)

![Bend, or Break](images/page036-206-img4.png)

![Bend, or Break](images/page036-206-img65.png)

![Bend, or Break](images/page036-206-img90.png)

---


> When we try to pick out anything by itself, we find it hitched to everything else in the Universe.
> ➤ John Muir
>
> Decoupled Code Is Easier to Change (Tip 44): Coupling is the enemy of change, because it links together things that must change in parallel.
> Law of Demeter: Don't talk to strangers. Only talk to your immediate collaborators.
> Avoid Train Wrecks: Chain of method calls is a sign of coupled code.
> Use Intefaces, Not Implementations: Program to an interface, not an implementation.

وقتی سعی می‌کنیم چیزی را به تنهایی انتخاب کنیم، می‌بینیم به همه چیزهای دیگر در جهان متصل است.
کد جداشده تغییر آن آسان‌تر است (نکته ۴۴): جفت‌شدن دشمن تغییر است، چون چیزهایی را که باید همزمان تغییر کنند به هم پیوند می‌دهد.
قانون دمیتر: با غریبه‌ها صحبت نکنید. فقط با همکاران مستقیم خود صحبت کنید.
از قطارهای شکسته اجتناب کنید: زنجیره فراخوانی‌های metod نشانه کد جفت‌شده است.
به interface برنامه‌نویسی کنید، نه پیاده‌سازی.

---

## ۲۹. دنیای واقعی را در دست بگیرید (Juggling the Real World)

> Events are the raw data of the real world. How we model and react to them has a profound effect on the resulting systems.
> Four Strategies for Handling Events:
> - Observer/Publish-Subscribe: Decouple event producers from consumers.
> - Mediator: Centralize event routing.
> - Event Sourcing: Record events, not state.
> - CQRS: Separate reads from writes.

رویدادها داده‌های خام دنیای واقعی هستند. نحوه مدل‌سازی و واکنش به آن‌ها تأثیر عمیقی بر سیستم‌های حاصل دارد.
چهار استراتژی برای مدیریت رویدادها:
- ناظر/انتشار-اشتراک: جفت‌کننده تولیدکنندگان و مصرف‌کنندگان رویداد را جدا کنید.
- واسطه: مسیریابی رویداد را متمرکز کنید.
- انتساب رویداد: رویدادها را ثبت کنید، نه وضعیت را.
- CQRS: خواندن‌ها را از نوشتن‌ها جدا کنید.

---

## ۳۰. تبدیل برنامه‌نویسی (Transforming Programming)

> Code that uses function pipelines tends to be clean, concise, and expressive. It's easy to understand what it does, and it's easy to change.
> pipelines are a natural way to express data transformations.
> Unlike method chains, pipelines pass data through functions without the objects knowing about each other.

کدی که از pipeline های تابعی استفاده می‌کند اغلب تمیز، مختصر و بیانگر است. آسان است بفهمید چه کاری انجام می‌دهد و آسان است تغییرش دهید.

---

## ۳۱. مالیات وراثت (Inheritance Tax)

> Inheritance can be overused. Favor composition over inheritance.
> Delegate, Don't Inherit: When you need to share functionality, consider using composition or delegation instead of inheritance.
> Use the Single Responsibility Principle: A class should have only one reason to change.

وراثت می‌تواند بیش از حد استفاده شود. ترکیب را بر وراثت ترجیح دهید.
واگذار کنید، وراثت ندهید: وقتی نیاز به اشتراک‌گذاری عملکرد دارید، ترکیب یا واگذاری را به جای وراثت در نظر بگیرید.
از اصل مسئولیت واحد استفاده کنید: یک کلاس باید فقط یک دلیل برای تغییر داشته باشد.

---

## ۳۲. پیکربندی (Configuration)

> Configuration is about moving details out of code, where they can be changed more safely and easily.
> Separate Configuration from Code: Configuration should be external to the code.
> Use Convention Over Configuration: When possible, use sensible defaults.
> Keep Configuration Close to the Data: If configuration changes with data, keep them together.

پیکربندی درباره خارج کردن جزئیات از کد است، جایی که می‌توان آن‌ها را با امنیت و آسان‌تر تغییر داد.
پیکربندی را از کد جدا کنید: پیکربندی باید خارج از کد باشد.
از قرارداد بر پیکربندی استفاده کنید: وقتی ممکن است، از پیش‌فرض‌های منطقی استفاده کنید.

---

# فصل ششم: همزمانی ⏱️ ۱۵ دقیقه مطالعه