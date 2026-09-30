> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی مقاله به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: مهندسان نرم‌افزار چگونه از مستندات استفاده می‌کنند

> **منبع اصلی:** How Software Engineers Use Documentation: The State of the Practice
> **نویسندگان:** T. C. Lethbridge, J. Singer, A. Forward
> **انتشار:** IEEE Software, Vol. 20, No. 6, November 2003, pp. 35–39
> **DOI:** 10.1109/MS.2003.1241364
> **لینک:** https://ieeexplore.ieee.org/document/1241364
> **نوع:** مقاله پژوهشی (Industry Study)

---

## چکیده

> Software engineering is a human task, and as such, we must study what software engineers do and think. Understanding the normative practice of software engineering is the first step toward developing realistic solutions to better facilitate the engineering process. We conducted three studies using several data-gathering approaches to elucidate the patterns by which software engineers (SEs) use documentation in their work. The studies confirm the widely held belief that most software engineers don't update most software documentation in a timely manner. The only notable exception is documentation types that are highly structured and easy to maintain, such as test cases and inline comments. The studies also show that engineers are generally favourably disposed to creating documentation, but they are constrained by the time they have available and by the tools at their disposal.

مهندسی نرم‌افزار یک کار انسانی است و به همین دلیل، باید مطالعه کنیم که مهندسان نرم‌افزار چه می‌کنند و چه می‌اندیشند. درک «عملِ هنجاری» مهندسی نرم‌افزار، نخستین گام برای توسعهٔ راه‌حل‌های واقع‌بینانه جهت تسهیل فرآیند مهندسی است. ما سه مطالعه با رویکردهای گوناگون گردآوری داده انجام دادیم تا الگوهایی را که مهندسان نرم‌افزار (SEs) بر پایهٔ آن‌ها در کار خود از مستندات استفاده می‌کنند روشن کنیم.

این مطالعات، باور رایج و پذیرفته‌شده را تأیید می‌کنند: بیشترِ مهندسان نرم‌افزار، بیشترِ مستندات نرم‌افزار را به‌موقع به‌روزرسانی نمی‌کنند. تنها استثنای قابل‌توجه، انواعی از مستندات است که **ساختاریافته** و **نگهداری‌شدنی** هستند؛ مانند test caseها و کامنت‌های inline. مطالعات همچنین نشان می‌دهند مهندسان عموماً نسبت به تولید مستندات دید مثبتی دارند، اما زمان در دسترس و ابزارهای در اختیارشان آن‌ها را محدود می‌کند.

---

## مسئله: «چقدر مستندات کافی است؟»

> Software engineering has been striving for years to improve the practice of software development and maintenance. Documentation has long been prominent on the list of recommended practices to improve development and help maintenance. Recently however, agile methods started to shake this view, arguing that the goal of the game is to produce software and that documentation is only useful as long as it helps to reach this goal.

مهندسی نرم‌افزار سال‌ها است می‌کوشد عملکرد توسعه و نگهداری نرم‌افزار را بهبود دهد. مستندسازی مدت‌ها در صدر فهرست شیوه‌های توصیه‌شده برای بهبود توسعه و کمک به نگهداری بوده است. اما اخیراً روش‌های چابک (Agile) این دیدگاه را به لرزه درآورده‌اند؛ با این استدلال که هدف بازی، تولید نرم‌افزار است و مستندسازی تنها تا زمانی مفید است که به رسیدن به آن هدف کمک کند.

> Documentation is a first class citizen in the software development process, and it is widely believed that good documentation is essential to the success of a software product. Yet when we look at industrial practice, the picture is less rosy.

مستندات یک شهروند درجه‌یک در فرآیند توسعهٔ نرم‌افزار است و به‌طور گسترده باور داریم که مستندات خوب برای موفقیت یک محصول نرم‌افزاری حیاتی است. اما وقتی به عملکرد واقعی صنعت نگاه می‌کنیم، تصویر چندان روشن نیست.

---

## روش‌شناسی: سه مطالعه صنعتی

> We conducted three studies using several data-gathering approaches to elucidate the patterns by which software engineers (SEs) use documentation in their work.

ما سه مطالعه با چندین رویکرد گردآوری داده انجام دادیم تا الگوهای استفادهٔ مهندسان نرم‌افزار از مستندات در کارشان روشن شود.

| نوع مطالعه | پرسش اصلی | خروجی |
|---|---|---|
| نظرسنجی (Survey) | مهندسان مستندات را **کِی** و **برای چه** می‌خوانند؟ | نقشهٔ نیازهای کاربر |
| مصاحبه (Interviews) | چرا مستندات را **نمی‌نویسند** یا **به‌روز نمی‌کنند**؟ | موانع فرهنگی و زمانی |
| مطالعهٔ تاریخی/لاگ (Log analysis) | در عمل **کدام** مستندات تولید می‌شوند؟ | شواهد عینی رفتار واقعی |

> Understanding the normative practice of software engineering is the first step toward developing realistic solutions to better facilitate the engineering process.

درک عمل هنجاریِ مهندسی نرم‌افزار، نخستین گام برای رسیدن به راه‌حل‌های واقع‌بینانه است. مقالهٔ حاضر، نقطهٔ شروعِ اکتشافی برای **مستندسازی مبتنی بر شواهد** (evidence-based documentation) است.

---

## یافتهٔ ۱: مستندات به‌موقع به‌روز نمی‌شوند

> The studies confirm the widely held belief that most software engineers don't update most software documentation in a timely manner.

مطالعات این باور رایج را تأیید می‌کنند که بیشترِ مهندسان، بیشترِ مستندات را به‌موقع به‌روز نمی‌کنند.

**معنای این یافته برای تیم‌ها:** اگر انتظار داشته باشید مستندات خودبه‌خود (self-updating) به‌روز شوند، ناامید خواهید شد. مستندات یک دارایی هستند که باید **بودجهٔ زمانی** برای نگهداری‌شان تخصیص دهید.

---

## یافتهٔ ۲: استثنای «ساختاریافته‌ها»

> The only notable exception is documentation types that are highly structured and easy to maintain, such as test cases and inline comments.

تنها استثنای قابل‌توجه، انواعی از مستندات است که **بسیار ساختاریافته** و **آسان برای نگهداری** هستند؛ مانند test caseها و کامنت‌های inline.

| مستند | چرا به‌روز می‌ماند؟ |
|---|---|
| **Test caseها** | اگر قدیمی شوند، **تست fail** می‌شود؛ سیستم خودش آن‌ها را فرزند نگه می‌دارد |
| **کامنت‌های inline** | در همان فایلی هستند که کد تغییر می‌کند؛ «هم‌مکانی» آن‌ها را همراه کد می‌آورد |
| **README / طراحی** | هیچ سازوکار اجباری برای همگام‌سازی ندارند؛ پس عقب می‌مانند |

> **نکتهٔ کلیدی:** «ساختاریافته بودن» = «اجباری بودنِ همگام‌سازی». هرچه مستند بیشتر به بازخورد خودکار گره بخورد، بیشتر زنده می‌ماند.

---

## یافتهٔ ۳: نگرش مثبت، ظرفیت محدود

> The studies also show that engineers are generally favourably disposed to creating documentation, but they are constrained by the time they have available and by the tools at their disposal.

مطالعات همچنین نشان می‌دهند مهندسان عموماً **تمایل مثبتی** به تولید مستندات دارند، اما **زمان در دسترس** و **ابزارهای موجود** آن‌ها را محدود می‌کند.

یعنی مشکل، **نگرش** نیست؛ **ظرفیت** است. این تفکیک مهمی است:

- ❌ «مهندسان مستندسازی را دوست ندارند» → غلط
- ✅ «مهندسان در یک sprint فشرده، اولویت را به کد می‌دهند» → درست

> **به زبان ساده:** اگر مستندسازی را به‌عنوان کاری *اضافه بر* کار جا بیندازید، هرگز انجام نمی‌شود. اگر آن را داخل خودِ جریان کد (commit، review، CI) جا بدهید، انجام می‌شود.

---

## نتیجه‌گیری و کاربرد عملی

> Understanding the normative practice of software engineering is the first step toward developing realistic solutions to better facilitate the engineering process.

درک عمل هنجاری، اولین گام است. بر این اساس، مقاله چند توصیهٔ مشخص ارائه می‌دهد:

1. **روی مستندات ساختاریافته سرمایه‌گذاری کنید** — چون خودشان را نگه می‌دارند (test، lint، docstring).
2. **مستندات را «بی‌زمان» ندانید** — برایشان وقت در برنامهٔ کاری رزرو کنید.
3. **ابزار را معیار قرار دهید** — هر مستندی که با کد هم‌مکان باشد، شانسِ بقای بیشتری دارد.
4. **مستندات را بسنجید** — همان‌طور که کیفیت کد را می‌سنجید، کیفیت مستندات را هم بسنجید.

> **میراث این مقاله:** مقالهٔ Lethbridge و همکاران (۲۰۰۳) سنگ‌بنای پژوهش تجربی در مستندسازی است. تقریباً هر مقالهٔ بعدی در این حوزه — از جمله مقالهٔ *Which documentation for software maintenance?* که در ادامهٔ همین مجموعه آمده — به این کار ارجاع می‌دهد.

---

## یادداشت شخصی

> **اهمیت این مقاله:** این مقاله نقطهٔ عطفی در پژوهش مستندسازی نرم‌افزار است. سه چیز را برای همیشه در ذهن من تثبیت کرد:
>
> **۱) مستندسازی یک مسئلهٔ اقتصادی است، نه انگیزشی.** مهندسان مستندات را دوست دارند؛ اما وقت ندارند. هر راه‌حلی که «زمان» کمتری بخواهد، شانس بیشتری دارد. این نگاه باعث شد به جای «چطور نویسندگان را متقاعد کنیم»، بپرسم «چطور اصولاً نیاز به نوشتن را حذف کنیم».
>
> **۲) هم‌مکانی، مهم‌تر از انگیزه است.** یافتهٔ استثناها (test case و کامنت inline) دقیقاً همان چیزی است که امروز به آن *docs-as-code* و *living documentation* می‌گویند. مقالهٔ ۲۰۰۳ عملاً پیش‌بینی کرده بود که راه‌حل، کم‌کردن فاصلهٔ ذهنی نویسنده و کد است.
>
> **۳) سنجش، تنها راه فرار از «مستندات خوب داریم» است.** جملهٔ «مستندات ما به‌روز است» یک ادعای احساسی است. تنها راه دفاع از آن، داشتن سیگنال است. این دقیقاً همان چیزی است که ۲۰ سال بعد در فصل ۷ کتاب *Software Engineering at Google* با نام Signals and Metrics پرداخته می‌شود.
>
> **چرا این منبع در کنار بقیهٔ این مجموعه مهم است:** دو مقالهٔ اول این مجموعه (این مقاله و *Which Documentation for Software Maintenance?*) پاسخ می‌دهند «واقعاً مهندسان چه می‌خواهند؟» و پنج مورد بعدی (Diátaxis، Docs Like Code، Living Documentation، Google Best Practices، Docs for Developers) پاسخ می‌دهند «پس چه باید کرد؟». این ترتیب عامدانه است: اول شواهد، بعد راه‌حل.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۹/۳۰
**منبع اصلی:** [IEEE Xplore - How Software Engineers Use Documentation](https://ieeexplore.ieee.org/document/1241364)
