> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۱۷۱

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

![Section](images/page001-171.png)

![Section](images/page002-172.png)

![Section](images/page003-173.png)

![Section](images/page004-174.png)

![Section](images/page005-175.png)

![Section](images/page006-176.png)

![Section](images/page007-177.png)

---

###### 📄 صفحه ۱۷۸

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

![Section](images/page008-178-img1.png)

![Section](images/page008-178-img2.png)

![Section](images/page008-178-img3.png)

![Section](images/page009-179-img1.png)

![Section](images/page009-179-img10.png)

![Section](images/page009-179-img11.png)

![Section](images/page009-179-img12.png)

![Section](images/page009-179-img13.png)

![Section](images/page009-179-img14.png)

![Section](images/page009-179-img15.png)

![Section](images/page009-179-img16.png)

![Section](images/page009-179-img17.png)

![Section](images/page009-179-img18.png)

![Section](images/page009-179-img19.png)

![Section](images/page009-179-img2.png)

![Section](images/page009-179-img20.png)

![Section](images/page009-179-img21.png)

![Section](images/page009-179-img22.png)

![Section](images/page009-179-img23.png)

![Section](images/page009-179-img24.png)

![Section](images/page009-179-img25.png)

![Section](images/page009-179-img26.png)

![Section](images/page009-179-img27.png)

![Section](images/page009-179-img28.png)

![Section](images/page009-179-img29.png)

![Section](images/page009-179-img3.png)

![Section](images/page009-179-img4.png)

![Section](images/page009-179-img5.png)

![Section](images/page009-179-img6.png)

![Section](images/page009-179-img7.png)

![Section](images/page009-179-img8.png)

![Section](images/page009-179-img9.png)

![Section](images/page010-180.png)

![Section](images/page011-181.png)

![Section](images/page012-182.png)

![Section](images/page013-183.png)

![Section](images/page014-184.png)

---

###### 📄 صفحه ۱۸۵

> Code that uses function pipelines tends to be clean, concise, and expressive. It's easy to understand what it does, and it's easy to change.
> pipelines are a natural way to express data transformations.
> Unlike method chains, pipelines pass data through functions without the objects knowing about each other.

کدی که از pipeline های تابعی استفاده می‌کند اغلب تمیز، مختصر و بیانگر است. آسان است بفهمید چه کاری انجام می‌دهد و آسان است تغییرش دهید.

![Section](images/page015-185.png)

![Section](images/page016-186-img1.png)

![Section](images/page017-187.png)

![Section](images/page018-188.png)

![Section](images/page019-189.png)

![Section](images/page020-190.png)

![Section](images/page021-191.png)

---

###### 📄 صفحه ۱۹۲

> Inheritance can be overused. Favor composition over inheritance.
> Delegate, Don't Inherit: When you need to share functionality, consider using composition or delegation instead of inheritance.
> Use the Single Responsibility Principle: A class should have only one reason to change.

وراثت می‌تواند بیش از حد استفاده شود. ترکیب را بر وراثت ترجیح دهید.
واگذار کنید، وراثت ندهید: وقتی نیاز به اشتراک‌گذاری عملکرد دارید، ترکیب یا واگذاری را به جای وراثت در نظر بگیرید.
از اصل مسئولیت واحد استفاده کنید: یک کلاس باید فقط یک دلیل برای تغییر داشته باشد.

![Section](images/page022-192.png)

![Section](images/page023-193.png)

![Section](images/page024-194.png)

![Section](images/page025-195.png)

![Section](images/page026-196.png)

![Section](images/page027-197.png)

![Section](images/page028-198.png)

---

###### 📄 صفحه ۱۹۹

> Configuration is about moving details out of code, where they can be changed more safely and easily.
> Separate Configuration from Code: Configuration should be external to the code.
> Use Convention Over Configuration: When possible, use sensible defaults.
> Keep Configuration Close to the Data: If configuration changes with data, keep them together.

پیکربندی درباره خارج کردن جزئیات از کد است، جایی که می‌توان آن‌ها را با امنیت و آسان‌تر تغییر داد.
پیکربندی را از کد جدا کنید: پیکربندی باید خارج از کد باشد.
از قرارداد بر پیکربندی استفاده کنید: وقتی ممکن است، از پیش‌فرض‌های منطقی استفاده کنید.

![Section](images/page029-199.png)

![Section](images/page030-200.png)

![Section](images/page031-201.png)

![Section](images/page032-202.png)

![Section](images/page033-203.png)

![Section](images/page034-204.png)

![Section](images/page035-205.png)

![Section](images/page036-206-img1.png)

![Section](images/page036-206-img10.png)

![Section](images/page036-206-img100.png)

![Section](images/page036-206-img101.png)

![Section](images/page036-206-img102.png)

![Section](images/page036-206-img103.png)

![Section](images/page036-206-img104.png)

![Section](images/page036-206-img105.png)

![Section](images/page036-206-img106.png)

![Section](images/page036-206-img107.png)

![Section](images/page036-206-img108.png)

![Section](images/page036-206-img109.png)

![Section](images/page036-206-img11.png)

![Section](images/page036-206-img110.png)

![Section](images/page036-206-img111.png)

![Section](images/page036-206-img112.png)

![Section](images/page036-206-img113.png)

![Section](images/page036-206-img114.png)

![Section](images/page036-206-img115.png)

![Section](images/page036-206-img116.png)

![Section](images/page036-206-img117.png)

![Section](images/page036-206-img118.png)

![Section](images/page036-206-img119.png)

![Section](images/page036-206-img12.png)

![Section](images/page036-206-img120.png)

![Section](images/page036-206-img121.png)

![Section](images/page036-206-img122.png)

![Section](images/page036-206-img123.png)

![Section](images/page036-206-img124.png)

![Section](images/page036-206-img125.png)

![Section](images/page036-206-img126.png)

![Section](images/page036-206-img127.png)

![Section](images/page036-206-img128.png)

![Section](images/page036-206-img129.png)

![Section](images/page036-206-img13.png)

![Section](images/page036-206-img130.png)

![Section](images/page036-206-img131.png)

![Section](images/page036-206-img132.png)

![Section](images/page036-206-img133.png)

![Section](images/page036-206-img134.png)

![Section](images/page036-206-img135.png)

![Section](images/page036-206-img136.png)

![Section](images/page036-206-img137.png)

![Section](images/page036-206-img138.png)

![Section](images/page036-206-img139.png)

![Section](images/page036-206-img14.png)

![Section](images/page036-206-img140.png)

![Section](images/page036-206-img141.png)

![Section](images/page036-206-img142.png)

![Section](images/page036-206-img143.png)

![Section](images/page036-206-img144.png)

![Section](images/page036-206-img145.png)

![Section](images/page036-206-img146.png)

![Section](images/page036-206-img147.png)

![Section](images/page036-206-img148.png)

![Section](images/page036-206-img149.png)

![Section](images/page036-206-img15.png)

![Section](images/page036-206-img150.png)

![Section](images/page036-206-img151.png)

![Section](images/page036-206-img152.png)

![Section](images/page036-206-img153.png)

![Section](images/page036-206-img154.png)

![Section](images/page036-206-img155.png)

![Section](images/page036-206-img156.png)

![Section](images/page036-206-img157.png)

![Section](images/page036-206-img158.png)

![Section](images/page036-206-img159.png)

![Section](images/page036-206-img16.png)

![Section](images/page036-206-img160.png)

![Section](images/page036-206-img161.png)

![Section](images/page036-206-img162.png)

![Section](images/page036-206-img163.png)

![Section](images/page036-206-img164.png)

![Section](images/page036-206-img165.png)

![Section](images/page036-206-img166.png)

![Section](images/page036-206-img167.png)

![Section](images/page036-206-img168.png)

![Section](images/page036-206-img169.png)

![Section](images/page036-206-img17.png)

![Section](images/page036-206-img170.png)

![Section](images/page036-206-img171.png)

![Section](images/page036-206-img172.png)

![Section](images/page036-206-img173.png)

![Section](images/page036-206-img174.png)

![Section](images/page036-206-img175.png)

![Section](images/page036-206-img176.png)

![Section](images/page036-206-img177.png)

![Section](images/page036-206-img178.png)

![Section](images/page036-206-img179.png)

![Section](images/page036-206-img18.png)

![Section](images/page036-206-img180.png)

![Section](images/page036-206-img181.png)

![Section](images/page036-206-img182.png)

![Section](images/page036-206-img183.png)

![Section](images/page036-206-img184.png)

![Section](images/page036-206-img185.png)

![Section](images/page036-206-img186.png)

![Section](images/page036-206-img187.png)

![Section](images/page036-206-img188.png)

![Section](images/page036-206-img189.png)

![Section](images/page036-206-img19.png)

![Section](images/page036-206-img190.png)

![Section](images/page036-206-img191.png)

![Section](images/page036-206-img192.png)

![Section](images/page036-206-img193.png)

![Section](images/page036-206-img194.png)

![Section](images/page036-206-img195.png)

![Section](images/page036-206-img196.png)

![Section](images/page036-206-img197.png)

![Section](images/page036-206-img198.png)

![Section](images/page036-206-img199.png)

![Section](images/page036-206-img2.png)

![Section](images/page036-206-img20.png)

![Section](images/page036-206-img200.png)

![Section](images/page036-206-img201.png)

![Section](images/page036-206-img202.png)

![Section](images/page036-206-img203.png)

![Section](images/page036-206-img204.png)

![Section](images/page036-206-img205.png)

![Section](images/page036-206-img206.png)

![Section](images/page036-206-img207.png)

![Section](images/page036-206-img208.png)

![Section](images/page036-206-img209.png)

![Section](images/page036-206-img21.png)

![Section](images/page036-206-img210.png)

![Section](images/page036-206-img211.png)

![Section](images/page036-206-img212.png)

![Section](images/page036-206-img213.png)

![Section](images/page036-206-img214.png)

![Section](images/page036-206-img215.png)

![Section](images/page036-206-img216.png)

![Section](images/page036-206-img217.png)

![Section](images/page036-206-img218.png)

![Section](images/page036-206-img219.png)

![Section](images/page036-206-img22.png)

![Section](images/page036-206-img220.png)

![Section](images/page036-206-img221.png)

![Section](images/page036-206-img222.png)

![Section](images/page036-206-img223.png)

![Section](images/page036-206-img224.png)

![Section](images/page036-206-img225.png)

![Section](images/page036-206-img226.png)

![Section](images/page036-206-img227.png)

![Section](images/page036-206-img228.png)

![Section](images/page036-206-img229.png)

![Section](images/page036-206-img23.png)

![Section](images/page036-206-img230.png)

![Section](images/page036-206-img231.png)

![Section](images/page036-206-img232.png)

![Section](images/page036-206-img233.png)

![Section](images/page036-206-img234.png)

![Section](images/page036-206-img235.png)

![Section](images/page036-206-img236.png)

![Section](images/page036-206-img237.png)

![Section](images/page036-206-img238.png)

![Section](images/page036-206-img239.png)

![Section](images/page036-206-img24.png)

![Section](images/page036-206-img240.png)

![Section](images/page036-206-img241.png)

![Section](images/page036-206-img242.png)

![Section](images/page036-206-img243.png)

![Section](images/page036-206-img244.png)

![Section](images/page036-206-img245.png)

![Section](images/page036-206-img246.png)

![Section](images/page036-206-img247.png)

![Section](images/page036-206-img248.png)

![Section](images/page036-206-img249.png)

![Section](images/page036-206-img25.png)

![Section](images/page036-206-img250.png)

![Section](images/page036-206-img251.png)

![Section](images/page036-206-img252.png)

![Section](images/page036-206-img253.png)

![Section](images/page036-206-img254.png)

![Section](images/page036-206-img255.png)

![Section](images/page036-206-img256.png)

![Section](images/page036-206-img257.png)

![Section](images/page036-206-img258.png)

![Section](images/page036-206-img259.png)

![Section](images/page036-206-img26.png)

![Section](images/page036-206-img260.png)

![Section](images/page036-206-img261.png)

![Section](images/page036-206-img262.png)

![Section](images/page036-206-img263.png)

![Section](images/page036-206-img264.png)

![Section](images/page036-206-img265.png)

![Section](images/page036-206-img266.png)

![Section](images/page036-206-img267.png)

![Section](images/page036-206-img268.png)

![Section](images/page036-206-img269.png)

![Section](images/page036-206-img27.png)

![Section](images/page036-206-img270.png)

![Section](images/page036-206-img271.png)

![Section](images/page036-206-img272.png)

![Section](images/page036-206-img273.png)

![Section](images/page036-206-img274.png)

![Section](images/page036-206-img275.png)

![Section](images/page036-206-img276.png)

![Section](images/page036-206-img277.png)

![Section](images/page036-206-img278.png)

![Section](images/page036-206-img279.png)

![Section](images/page036-206-img28.png)

![Section](images/page036-206-img280.png)

![Section](images/page036-206-img281.png)

![Section](images/page036-206-img29.png)

![Section](images/page036-206-img3.png)

![Section](images/page036-206-img30.png)

![Section](images/page036-206-img31.png)

![Section](images/page036-206-img32.png)

![Section](images/page036-206-img33.png)

![Section](images/page036-206-img34.png)

![Section](images/page036-206-img35.png)

![Section](images/page036-206-img36.png)

![Section](images/page036-206-img37.png)

![Section](images/page036-206-img38.png)

![Section](images/page036-206-img39.png)

![Section](images/page036-206-img4.png)

![Section](images/page036-206-img40.png)

![Section](images/page036-206-img41.png)

![Section](images/page036-206-img42.png)

![Section](images/page036-206-img43.png)

![Section](images/page036-206-img44.png)

![Section](images/page036-206-img45.png)

![Section](images/page036-206-img46.png)

![Section](images/page036-206-img47.png)

![Section](images/page036-206-img48.png)

![Section](images/page036-206-img49.png)

![Section](images/page036-206-img5.png)

![Section](images/page036-206-img50.png)

![Section](images/page036-206-img51.png)

![Section](images/page036-206-img52.png)

![Section](images/page036-206-img53.png)

![Section](images/page036-206-img54.png)

![Section](images/page036-206-img55.png)

![Section](images/page036-206-img56.png)

![Section](images/page036-206-img57.png)

![Section](images/page036-206-img58.png)

![Section](images/page036-206-img59.png)

![Section](images/page036-206-img6.png)

![Section](images/page036-206-img60.png)

![Section](images/page036-206-img61.png)

![Section](images/page036-206-img62.png)

![Section](images/page036-206-img63.png)

![Section](images/page036-206-img64.png)

![Section](images/page036-206-img65.png)

![Section](images/page036-206-img66.png)

![Section](images/page036-206-img67.png)

![Section](images/page036-206-img68.png)

![Section](images/page036-206-img69.png)

![Section](images/page036-206-img7.png)

![Section](images/page036-206-img70.png)

![Section](images/page036-206-img71.png)

![Section](images/page036-206-img72.png)

![Section](images/page036-206-img73.png)

![Section](images/page036-206-img74.png)

![Section](images/page036-206-img75.png)

![Section](images/page036-206-img76.png)

![Section](images/page036-206-img77.png)

![Section](images/page036-206-img78.png)

![Section](images/page036-206-img79.png)

![Section](images/page036-206-img8.png)

![Section](images/page036-206-img80.png)

![Section](images/page036-206-img81.png)

![Section](images/page036-206-img82.png)

![Section](images/page036-206-img83.png)

![Section](images/page036-206-img84.png)

![Section](images/page036-206-img85.png)

![Section](images/page036-206-img86.png)

![Section](images/page036-206-img87.png)

![Section](images/page036-206-img88.png)

![Section](images/page036-206-img89.png)

![Section](images/page036-206-img9.png)

![Section](images/page036-206-img90.png)

![Section](images/page036-206-img91.png)

![Section](images/page036-206-img92.png)

![Section](images/page036-206-img93.png)

![Section](images/page036-206-img94.png)

![Section](images/page036-206-img95.png)

![Section](images/page036-206-img96.png)

![Section](images/page036-206-img97.png)

![Section](images/page036-206-img98.png)

![Section](images/page036-206-img99.png)

---
