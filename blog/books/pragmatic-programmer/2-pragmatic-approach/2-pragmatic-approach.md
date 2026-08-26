> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۵۷

> Good Design Is Easier to Change Than Bad Design (Tip 14): A thing is well designed if it adapts to the people who use it. For code, that means it must adapt by changing. So we believe in the ETC principle: Easier to Change. ETC. That's it.
> As far as we can tell, every design principle out there is a special case of ETC. Why is decoupling good? Because by isolating concerns we make each easier to change. ETC. Why is the single responsibility principle useful? Because a change in requirements is mirrored by a change in just one module. ETC. Why is naming important? Because good names make code easier to read, and you have to read it to change it. ETC!
> ETC Is a Value, Not a Rule: Values are things that help you make decisions. When it comes to thinking about software, ETC is a guide, helping you choose between paths.

طراحی خوب تغییر آن بد است آسان‌تر است (نکته ۱۴): یک چیز خوب طراحی شده است اگر با افرادی که از آن استفاده می‌کنند سازگار شود. برای کد، این به این معنی است که باید با تغییر سازگار شود. پس ما به اصل ETC اعتقاد داریم: آسان‌تر برای تغییر. ETC. همین.
به نظر ما، هر اصل طراحی‌ای که وجود دارد حالت خاصی از ETC است. چرا جداسازی خوب است؟ چون با جدا کردن نگرانی‌ها، هر کدام را آسان‌تر برای تغییر می‌کنیم. ETC. چرا اصل مسئولیت واحد مفید است؟ چون تغییر در نیازمندی‌ها فقط در یک ماژول منعکس می‌شود. ETC. چرا نام‌گذاری مهم است؟ چون نام‌های خوب کد را آسان‌تر برای خواندن می‌کنند و باید بخوانیدش تا تغییرش دهید. ETC!
ETC یک ارزش است، نه یک قاعده: ارزش‌ها چیزهایی هستند که به شما در تصمیم‌گیری کمک می‌کنند.

![Section](images/page001-057.png)

![Section](images/page002-058.png)

![Section](images/page003-059.png)

![Section](images/page004-060-img1.png)

![Section](images/page004-060-img2.png)

![Section](images/page005-061.png)

---

###### 📄 صفحه ۶۲

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.
> DRY—Don't Repeat Yourself (Tip 15): The alternative is to have the same thing expressed in two or more places. If you change one, you have to remember to change the others, or your program will be brought to its knees by a contradiction.
> DRY Is More Than Code: DRY is about the duplication of knowledge, of intent. It's about expressing the same thing in two different places, possibly in two totally different ways.
> Not All Code Duplication Is Knowledge Duplication: The code is the same, but the knowledge they represent is different. The two functions validate two separate things that just happen to have the same rules. That's a coincidence, not a duplication.
> Make It Easy to Reuse (Tip 16): What you're trying to do is foster an environment where it's easier to find and reuse existing stuff than to write it yourself.

هر قطعه دانش باید یک نمایش واحد، غیرمبهم و معتبر درون یک سیستم داشته باشد.
DRY — تکرار نکنید (نکته ۱۵): جایگزین این است که یک چیز در دو یا چند جا بیان شده باشد. اگر یکی را تغییر دهید، باید به یاد داشته باشید بقیه را هم تغییر دهید، وگرنه برنامه‌تان با تناقض زمین می‌خورد.
DRY فقط کد نیست: DRY درباره تکرار دانش، نیت است. درباره بیان یک چیز در دو جای مختلف است، احتمالاً به دو روش کاملاً متفاوت.
هر تکرار کدی تکرار دانش نیست: کد یکسان است، اما دانشی که نشان می‌دهند متفاوت است.
استفاده مجدد را آسان کنید (نکته ۱۶): هدف شما ایجاد محیطی است که در آن پیدا کردن و استفاده مجدد از چیزهای موجود آسان‌تر از نوشتن خودتان باشد.

![Section](images/page006-062.png)

![Section](images/page007-063.png)

![Section](images/page008-064.png)

![Section](images/page009-065.png)

![Section](images/page010-066.png)

---

###### 📄 صفحه ۶۷

> Orthogonality is a critical concept if you want to produce systems that are easy to design, build, test, and extend. In computing, the term has come to signify a kind of independence or decoupling. Two or more things are orthogonal if changes in one do not affect any of the others.
> Eliminate Effects Between Unrelated Things (Tip 17): We want to design components that are self-contained: independent, and with a single, well-defined purpose.
> Benefits of Orthogonality:
> - Gain Productivity: Changes are localized, so development time and testing time are reduced.
> - Reduce Risk: Diseased sections of code are isolated. The resulting system is less fragile.
> Keep your code decoupled. Write shy code—modules that don't reveal anything unnecessary to other modules.

قطعیت مفهومی حیاتی است اگر می‌خواهید سیستم‌هایی تولید کنید که طراحی، ساخت، تست و گسترش آن‌ها آسان باشد. در محاسبات، این اصطلاح به نوعی استقلال یا جداسازی اشاره کرده است.
اثرات بین چیزهای نامرتبط را حذف کنید (نکته ۱۷): می‌خواهیم مولفه‌هایی طراحی کنیم که خودکفا باشند: مستقل، و با هدف واحد و مشخص.
مزایای قطعیت:
- بهره‌وری افزایش می‌یابد: تغییرات محلی هستند، بنابراین زمان توسعه و تست کاهش می‌یابد.
- ریسک کاهش می‌یابد: بخش‌های آلوده کد جدا می‌شوند. سیستم حاصل شکننده‌تر است.
کدتان را جدا نگه دارید. کد خجالتی بنویسید — ماژول‌هایی که چیز غیرضروری به ماژول‌های دیگر نشان نمی‌دهند.

![Section](images/page011-067.png)

![Section](images/page012-068.png)

![Section](images/page013-069.png)

![Section](images/page014-070.png)

![Section](images/page015-071.png)

---

###### 📄 صفحه ۷۲

> Nothing is more dangerous than an idea if it’s the only one you have.
> ➤ Emil-Auguste Chartier (Alain)
> 
> There Are No Final Decisions (Tip 18): Many of the topics in this book are geared to producing flexible, adaptable software. By sticking to their recommendations—especially the DRY principle, decoupling, and use of external configuration—we don't have to make as many critical, irreversible decisions.
> Flexible Architecture: How can you plan for architectural volatility? You can't. What you can do is make it easy to change. Hide third-party APIs behind your own abstraction layers.
> Forgo Following Fads (Tip 19): No one knows what the future may hold, especially not us! So enable your code to rock-n-roll.

هیچ چیز خطرناک‌تر از یک ایده نیست اگر تنها ایده‌ای باشد که دارید.
هیچ تصمیم نهایی وجود ندارد (نکته ۱۸): بسیاری از موضوعات این کتاب برای تولید نرم‌افزار انعطاف‌پذیر و سازگار هستند. با پایبندی به توصیه‌های آن‌ها — به ویژه اصل DRY، جداسازی و استفاده از پیکربندی خارجی — مجبور نیستیم تصمیمات حیاتی و غیرقابل بازگشت زیادی بگیریم.
معماری انعطاف‌پذیر: چگونه برای نوسانات معماری برنامه‌ریزی کنید؟ نمی‌توانید. کاری که می‌توانید انجام دهید این است که تغییر را آسان کنید.
از ترند‌ها پیروی نکنید (نکته ۱۹): هیچ‌کس نمی‌داند آینده چه خواهد داشت، مخصوصاً ما! پس به کدتان اجازه رقص بدهید.

![Section](images/page016-072.png)

![Section](images/page017-073-img1.png)

![Section](images/page017-073-img2.png)

![Section](images/page017-073-img3.png)

![Section](images/page017-073-img4.png)

![Section](images/page017-073-img5.png)

![Section](images/page017-073-img6.png)

![Section](images/page017-073-img7.png)

![Section](images/page018-074.png)

![Section](images/page019-075.png)

![Section](images/page020-076.png)

---

###### 📄 صفحه ۷۷

> Ready, fire, aim…
> ➤ Anon
> 
> Use Tracer Bullets to Find the Target (Tip 20): In fact, given the complexity of today's project setup, with swarms of external dependencies and tools, tracer bullets become even more important.
> Tracer code is not disposable: you write it for keeps. It contains all the error checking, structuring, documentation, and self-checking that any piece of production code has. It simply is not fully functional.
> Tracer Bullets Don't Always Hit Their Target: Tracer bullets show what you're hitting. This may not always be the target. You then adjust your aim until they're on target.
> Tracer Code versus Prototyping: Prototyping generates disposable code. Tracer code is lean but complete, and forms part of the skeleton of the final system.

آماده، شلیک، هدف‌گیری…
از گلوله‌های ردیاب برای یافتن هدف استفاده کنید (نکته ۲۰): در واقع، با توجه به پیچیدگی تنظیمات پروژه‌های امروزی، با انبوهی از وابستگی‌ها و ابزارهای خارجی، گلوله‌های ردیاب حتی مهم‌تر می‌شوند.
کد ردیاب قابل دور ریختن نیست: آن را برای همیشه می‌نویسید. تمام بررسی‌های خطا، ساختاربندی، مستندات و خودبررسی را دارد.
گلوله‌های ردیاب همیشه به هدف نمی‌خورند: گلوله‌های ردیاب نشان می‌دهند به چه چیزی می‌خورید. این ممکن است همیشه هدف نباشد. سپس هدف‌گیری خود را تنظیم می‌کنید.
کد ردیاب در مقابل پروتوتایپ: پروتوتایپ کد قابل دور ریختن تولید می‌کند. کد ردیاب لاغر اما کامل است و بخشی از اسکلت سیستم نهایی را تشکیل می‌دهد.

![Section](images/page021-077.png)

![Section](images/page022-078.png)

![Section](images/page023-079.png)

![Section](images/page024-080.png)

![Section](images/page025-081.png)

---

###### 📄 صفحه ۸۲

> Many industries use prototypes to try out specific ideas; prototyping is much cheaper than full-scale production.
> Prototype to Learn (Tip 21): Prototyping is a learning experience. Its value lies not in the code produced, but in the lessons learned.
> Things to Prototype: Architecture, new functionality, structure or contents of external data, third-party tools or components, performance issues, user interface design.
> How to Use Prototypes: Ignore correctness, completeness, robustness, and style. Prototypes gloss over details, and focus in on specific aspects of the system.
> How Not to Use Prototypes: Before you embark on any code-based prototyping, make sure that everyone understands that you are writing disposable code.

بسیاری از صنایع از پروتوتایپ‌ها برای آزمایش ایده‌های خاص استفاده می‌کنند؛ پروتوتایپ‌سازی بسیار ارزان‌تر از تولید تمام‌عیار است.
برای یادگیری پروتوتایپ بسازید (نکته ۲۱): پروتوتایپ‌سازی یک تجربه یادگیری است. ارزش آن نه در کد تولید شده، بلکه در درس‌های آموخته شده است.
چیزهایی برای پروتوتایپ: معماری، عملکرد جدید، ساختار یا محتوای داده‌های خارجی، ابزارهای یا مولفه‌های شخص ثالث، مسائل عملکرد، طراحی رابط کاربری.
نحوه استفاده از پروتوتایپ‌ها: از صحت، کامل بودن، استحکام و سبک چشم‌پوشی کنید.
نحوه عدم استفاده از پروتوتایپ‌ها: قبل از شروع هر پروتوتایپ‌سازی مبتنی بر کد، مطمئن شوید همه درک می‌کنند که کد قابل دور ریختن می‌نویسید.

![Section](images/page026-082.png)

![Section](images/page027-083.png)

![Section](images/page028-084.png)

![Section](images/page029-085.png)

![Section](images/page030-086.png)

---

###### 📄 صفحه ۸۷

> The limits of my language are the limits of my world.
> ➤ Ludwig Wittgenstein
> 
> Much as you may like to just say "make it so" and have the computer build your application, in many cases you can get at least partway there. Use and build domain languages.
> Domain-Specific Languages (Tip 22): Programming in a small, domain-specific language is often simpler and more natural than programming in a general-purpose language.

محدودیت‌های زبان من، محدودیت‌های دنیای من است.
زبان‌های خاص دامنه (نکته ۲۲): برنامه‌نویسی در یک زبان کوچک و خاص دامنه اغلب ساده‌تر و طبیعی‌تر از برنامه‌نویسی در یک زبان عمومی است.

![Section](images/page031-087.png)

![Section](images/page032-088.png)

![Section](images/page033-089.png)

![Section](images/page034-090.png)

![Section](images/page035-091.png)

---

###### 📄 صفحه ۹۲

> Estimating is the process of finding an approximation, which is a value that is usable for some purpose even if input data may be incomplete, uncertain, or unstable.
> The Computer Delivers Pizza (Tip 23): Often, when estimating time to do technical tasks, the answer is a complex function of many variables.
> Estimate the Scope of the Work: Break the problem down into smaller pieces. Each component is easier to estimate, and you can add up the estimates.
> Build Estimates from the Bottom Up: Start with the small tasks, and add them up.
> Know When to Leave It Alone: Don't spend too much time on the estimate. It's an approximation, not a commitment.

تخمین فرآیند یافتن تقریبی است که مقداری است که برای برخی اهداف قابل استفاده است حتی اگر داده‌های ورودی ناقص، نامطمئن یا ناپایدار باشند.
کامپیوتر پیتزا تحویل می‌دهد (نکته ۲۳): اغلب، هنگام تخمین زمان برای انجام وظایف فنی، پاسخ تابع پیچیده‌ای از متغیرهای زیادی است.
دامنه کار را تخمین بزنید: مشکل را به قطعات کوچکتر تقسیم کنید.
تخمین‌ها را از پایین به بالا بسازید: با وظایف کوچک شروع کنید و آن‌ها را جمع کنید.
بدانید چه زمانی رهایش کنید: وقت زیادی برای تخمین صرف نکنید.

![Section](images/page036-092.png)

![Section](images/page037-093.png)

![Section](images/page038-094.png)

![Section](images/page039-095.png)

![Section](images/page040-096.png)

![Section](images/page041-097.png)

![Section](images/page042-098.png)

![Section](images/page043-099.png)

![Section](images/page044-100.png)

---
