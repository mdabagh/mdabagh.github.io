> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی راهنما به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: بهترین شیوه‌های مستندسازی — Google Style Guide

> **منبع اصلی:** Google Documentation Best Practices (Google Developer Documentation Style Guide)
> **ناشر:** Google
> **لینک:** https://google.github.io/styleguide/docguide/best_practices.html
> **نوع:** راهنمای رسمی (متن‌باز — CC BY 3.0)

---

## چکیده

> "Say what you mean, simply and directly." — Brian Kernighan

**«بگو منظورت چیست، به‌سادگی و مستقیم.»** — برایان کرنیگان

> A small set of fresh and accurate docs is better than a large assembly of "documentation" in various states of disrepair.
> **Docs work best when they are alive but frequently trimmed, like a bonsai tree.**

مجموعه‌ای کوچک از مستندات **تازه و دقیق**، بهتر از مجموعه‌ای بزرگ از «مستندات» با وضعیت‌های گوناگون خرابی است.

**مستندات زمانی بهترین کار می‌کنند که زنده باشند، اما مدام هرس شوند — درست مثل درخت بونسای.**

---

## ۱. کمترین مستنداتِ قابل‌قبول (Minimum Viable Documentation)

> A small set of fresh and accurate docs is better than a large assembly of "documentation" in various states of disrepair.
> Write short and useful documents. Cut out everything unnecessary, including out-of-date, incorrect, or redundant information. Also make a habit of continually massaging and improving every doc to suit your changing needs. **Docs work best when they are alive but frequently trimmed, like a bonsai tree**.

مجموعه‌ای کوچک از مستندات تازه و دقیق، بهتر از مجموعه‌ای بزرگ از «مستندات» با وضعیت‌های گوناگون خرابی است.

**سندهای کوتاه و مفید بنویسید.** هر چیز غیرضروری را حذف کنید — از جمله اطلاعات منسوخ، نادرست یا تکراری. همچنین عادت کنید که هر سند را به‌طور مستمر پالایش و بهبود دهید تا با نیازهای در حال تغییر شما بخواند.

> **مستندات زمانی بهترین کار می‌کنند که زنده باشند، اما مدام هرس شوند — درست مثل درخت بونسای.**

> **به زبان ساده:** بونسای یعنی درختی که هر بار **کوچک‌ترش می‌کنی** تا شکل زیباتری پیدا کند. استعارهٔ گوگل یعنی: حجم زیاد نشانهٔ کیفیت نیست. هر سندی که نتوانید حذفش کنید، بهتر است اصلاً ننویسید.

### اصل کلیدی

> **حجم، معیار نیست. تازگی معیار است.**

| مستندات ۱۰۰ صفحه‌ای منسوخ | مستندات ۳ صفحه‌ای دقیق |
|---|---|
| اعتماد می‌شود، پس غلط می‌دهد | اعتماد می‌شود، پس درست راهنمایی می‌کند |
| هزینهٔ نگهداری سنگین | هزینهٔ نگهداری سبک |
| ❌ خطرناک‌تر | ✅ مفید |

---

## ۲. به‌روزرسانی مستندات هم‌زمان با کد

> **Change your documentation in the same CL as the code change**. This keeps your docs fresh, and is also a good place to explain to your reviewer what you're doing.

**مستندات خود را در همان CL (Change List / Pull Request) که کد را تغییر می‌دهید، تغییر دهید.** این کار مستندات را تازه نگه می‌دارد و جای خوبی هم برای توضیح به بازبینی است که چه می‌کنید.

> A good reviewer can at least insist that docstrings, header files, README.md files, and any other docs get updated alongside the CL.

یک بازبینی خوب حداقل می‌تواند اصرار کند که docstringها، فایل‌های هدر، فایل‌های `README.md` و هر مستند دیگری، هم‌زمان با CL به‌روزرسانی شوند.

> **نکتهٔ کلیدی:** کلمهٔ «حداقل» مهم است. بازبین نمی‌تواند جلوی کسی را که اصلاً فکر نمی‌کند بگیرد، اما **می‌تواند** سازوکاری باشد که فکر کردن را اجباری کند. این یک اهرم قدرت نرم است، نه یک قانون سخت.
>
> **هم‌راستا با یافتهٔ مقالهٔ [Lethbridge et al. 2003](https://ieeexplore.ieee.org/document/1241364):** آن مقاله نشان داد مشکل مستندات، **نگرش** نیست، **ظرفیت** است. CL ترکیبی، ظرفیت اضافه نمی‌خواهد — فقط ترتیب کار را عوض می‌کند.

---

## ۳. حذف مستندات مرده

> Dead docs are bad. They misinform, they slow down, they incite despair in engineers and laziness in team leads. They set a precedent for leaving behind messes in a code base. If your home is clean, most guests will be clean without being asked.

**مستندات مرده بد هستند.** آن‌ها اطلاعات نادرست می‌دهند، کار را کند می‌کنند، در مهندسان ناامیدی و در سرپرستان تیم تنبلی ایجاد می‌کنند. این‌ها سابقه‌ای می‌سازند که آشفتگی در کد‌بیس جا گذاشته شود. اگر خانه‌ات تمیز باشد، بیشتر مهمان‌ها بدون آنکه بخواهی تمیز رفتار می‌کنند.

> Just like any big cleaning project, **it's easy to be overwhelmed**. If your docs are in bad shape:
> - Take it slow, doc health is a gradual accumulation.
> - First delete what you're certain is wrong, ignore what's unclear.
> - Get your whole team involved. Devote time to quickly scan every doc and make a simple decision: Keep or delete?
> - Default to delete or leave behind if migrating. Stragglers can always be recovered.
> - Iterate.

درست مثل هر پروژهٔ بزرگ نظافت، **غلبه بر آن آسان نیست**. اگر مستنداتت در وضعیت بدی هستند:
- **آرام پیش برو** — سلامت مستندات انباشت تدریجی است.
- **اول آنچه مطمئنی غلط است حذف کن**؛ آنچه نامشخص است را نادیده بگیر.
- **کل تیمت را درگیر کن.** وقتی بگذار تا سریع همهٔ مستندات را اسکن کنند و تصمیم ساده‌ای بگیرند: **نگه دارم یا حذف کنم؟**
- **در هنگام مهاجرت، پیش‌فرض را «حذف یا رها کردن» بگذار.** آنچه جا مانده را همیشه می‌توان بازیابی کرد.
- **تکرار کن (Iterate).**

> **به زبان ساده:** پاکسازیِ یک‌باره جواب نمی‌دهد، چون حجمش وحشتناک است. اما یک «دور» ۹۰ دقیقه‌ای هفتگی، بعد از چند ماه وضعیت را عوض می‌کند. نکتهٔ کلیدی، گزینهٔ «نامشخص» است: تصمیم نگیر و رها کن، چون وقتِ تصمیم‌گیری نداری و مهم‌تر از این، سندِ مرده بهتر از «نیمه‌تصمیم» است.

---

## ۴. خوب، بهتر از کامل است

> Documentation is an art. There is no perfect document, there are only proven methods and prudent guidelines.

**مستندسازی یک هنر است.** سندِ کامل وجود ندارد؛ تنها روش‌های آزموده و رهنمودهای محتاطانه وجود دارد.

> **به زبان ساده:** کمال‌گرایی، دشمنِ انتشار است. سندِ ۸۰ درصدِ خوب، ۱۰ برابر ارزشمندتر از سندِ ۱۰۰ درصدِ عالی‌ای است که هرگز منتشر نمی‌شود.

---

## ۵. مستندات، داستان کد شما هستند

> Writing excellent code doesn't end when your code compiles or even if your test coverage reaches 100%. It's easy to write something a computer understands, it's much harder to write something both a human and a computer understand. Your mission as a Code Health-conscious engineer is to **write for humans first, computers second.** Documentation is an important part of this skill.

نوشتن کد عالی وقتی تمام نمی‌شود که کدت کامپایل می‌شود یا حتی وقتی پوشش تست به ۱۰۰٪ می‌رسد. نوشتن چیزی که **کامپیوتر** بفهمد آسان است؛ نوشتن چیزی که **هم انسان و هم کامپیوتر** بفهمند بسیار سخت‌تر است. مأموریت شما به‌عنوان مهندسی آگاه به سلامت کد این است: **اول برای انسان‌ها بنویس، بعد برای کامپیوتر.** مستندسازی بخش مهمی از این مهارت است.

> There's a spectrum of engineering documentation that ranges from terse comments to detailed prose:

طیفی از مستندسازی مهندسی وجود دارد که از کامنت‌های کوتاه تا نوشتار مفصل گسترده می‌شود:

---

### ۱. نام‌های معنادار

> Good naming allows the code to convey information that would otherwise be relegated to comments or documentation. This includes nameable entities at all levels, from local variables to classes, files, and directories.

**نام‌گذاری خوب** اجازه می‌دهد کد اطلاعاتی را منتقل کند که در غیر این صورت ناچار به کامنت یا مستند می‌شد. این شامل موجودیت‌های نام‌پذیر در همهٔ سطوح است: از متغیرهای محلی تا کلاس‌ها، فایل‌ها و پوشه‌ها.

> **به زبان ساده:** نام خوب، **مستندِ رایگان** است. `process(items)` هیچ نمی‌گوید. `filterExpiredAndDeduplicateOrders(orders)` هم **مستند** است و هم **کد**. این بالاترین نقطهٔ بازگشت سرمایه‌گذاری در مستندسازی است.

---

### ۲. کامنت‌های درون‌خطی

> The primary purpose of inline comments is to provide information that the code itself cannot contain, such as why the code is there.

**هدف اصلی کامنت‌های درون‌خطی**، دادن اطلاعاتی است که **خودِ کد نمی‌تواند در خود داشته باشد** — مثلاً **چرا** کد آنجاست.

> **قاعدهٔ ساده:** اگر کامنتت دارای «چرا» است، نگهش دار. اگر «چه» است، یا کد را بدهکار خودت کن (اگر خوانا نیست) یا حذفش کن.

---

### ۳. مستندات API متد و کلاس

> **Method API documentation**: The header / Javadoc / docstring comments that say what methods do and how to use them. This documentation is **the contract of how your code must behave**. The intended audience is future programmers who will use and modify your code.

**مستندات API متد:** کامنت‌های هدر / Javadoc / docstring که می‌گویند متدها چه می‌کنند و چگونه استفاده می‌شوند. این مستندات **قرارداد** نحوهٔ رفتار کد شما هستند. مخاطب هدف، برنامه‌نویسان آینده‌ای هستند که از کد شما استفاده و آن را تغییر می‌دهند.

> It is often reasonable to say that any behavior documented here should have a test verifying it. This documentation details what arguments the method takes, what it returns, any "gotchas" or restrictions, and what exceptions it can throw or errors it can return. It does not usually explain why code behaves a particular way unless that's relevant to a developer's understanding of how to use the method. "Why" explanations are for inline comments. Think in practical terms when writing method documentation: "This is a hammer. You use it to pound nails."

معمولاً منطقی است بگوییم هر رفتاری که اینجا مستند شده، باید یک تست تأییدکننده داشته باشد. این مستندات جزئیات می‌دهند از: متد چه آرگومان‌هایی می‌گیرد، چه چیزی برمی‌گرداند، چه «دام‌ها» یا محدودیت‌هایی دارد، و چه استثناهایی می‌تواند پرتاب کند. معمولاً توضیح نمی‌دهد **چرا** کد به شکل خاصی رفتار می‌کند، مگر اینکه برای فهم توسعه‌دهنده از نحوهٔ استفاده از متد مرتبط باشد. توضیح «چرا» برای کامنت‌های درون‌خطی است. هنگام نوشتن مستندات متد، عملی فکر کن: «**این یک چکش است. از آن برای کوبدن میخ استفاده می‌کنی.**»

> **این جمله، حکمت کل فصل است:** مستندات خوب، **متشابه‌سازی روشن** هستند، نه توصیف دقیق.

> **Class / Module API documentation**: The header / Javadoc / docstring comments for a class or a whole file. This documentation gives a brief overview of what the class / file does and often gives a few short examples of how you might use the class / file.
> Examples are particularly relevant when there's several distinct ways to use the class (some advanced, some simple). Always list the simplest use case first.

**مستندات کلاس / ماژول:** کامنت‌های هدر برای یک کلاس یا کل فایل. این مستندات نمای کلی کوتاهی از کار کلاس/فایل می‌دهند و اغلب چند مثال کوتاه از نحوهٔ استفاده ارائه می‌کنند. مثال‌ها وقتی بسیار مرتبط‌اند که روش‌های متمایزی برای استفاده از کلاس وجود داشته باشد. **همیشه ساده‌ترین حالت کاربرد را اول فهرست کنید.**

---

### ۴. فایل README.md

> A good README.md orients the new user to the directory and points to more detailed explanation and user guides:
> - What is this directory intended to hold?
> - Which files should the developer look at first? Are some files an API?
> - Who maintains this directory and where I can learn more?

یک `README.md` خوب، کاربر جدید را نسبت به پوشه جهت‌دهی می‌کند و به توضیحات مفصل‌تر و راهنماهای کاربری اشاره می‌کند:
- این پوشه قرار است چه چیزی را در خود نگه دارد؟
- توسعه‌دهنده باید اول کدام فایل‌ها را ببیند؟ آیا بعضی فایل‌ها API هستند؟
- چه کسی از این پوشه نگهداری می‌کند و کجا می‌توانم بیشتر بدانم؟

> **نکته:** README پاسخ به پرسش «**کجا**» است، نه «**چگونه**». اگر محتوای README بیش از یک صفحه شد، وقت آن است که به `docs/` مهاجرت کند.

---

### ۵. پوشهٔ docs

> The contents of a good docs directory explain how to:
> - Get started using the relevant API, library, or tool.
> - Run its tests.
> - Debug its output.
> - Release the binary.

محتوای یک پوشهٔ `docs` خوب توضیح می‌دهد که چگونه:
- با API، کتابخانه یا ابزار مربوطه **شروع** کنیم
- **تست‌هایش** را اجرا کنیم
- **خروجی‌اش** را عیب‌یابی کنیم
- **باینری** را منتشر کنیم

> **دقیقاً همان ساختاری که مستندات هر زبان برنامه‌نویسیِ بالغی دارد.** هر زبانی که این چهار را دارد، بالغ است.

---

### ۶-۷. اسناد طراحی، PRD و مستندات بیرونی

> **Design docs, PRDs**: A good design doc or PRD discusses the proposed implementation at length for the purpose of collecting feedback on that design. However, once the code is implemented, design docs should serve as **archives of these decisions**, not as half-correct docs (they are often misused).

**اسناد طراحی و PRD:** یک سند طراحی یا PRD خوب، پیاده‌سازی پیشنهادی را به‌طور مفصل بحث می‌کند تا بازخورد جمع‌آوری شود. اما پس از پیاده‌سازی کد، اسناد طراحی باید **آرشیو تصمیم‌ها** باشند، نه سندهای نیمه‌درست (که اغلب بد استفاده می‌شوند).

> **Other external docs**: Some teams maintain documentation in other locations, separate from the code, such as Google Sites, Drive, or wiki. If you do maintain documentation in other locations, you should clearly point to those locations from your project directory.

**مستندات بیرونی:** برخی تیم‌ها مستندات را در مکان‌های دیگری جدا از کد نگهداری می‌کنند. اگر چنین می‌کنید، باید از پوشهٔ پروژه به‌وضوح به آن مکان‌ها اشاره کنید.

> **نکتهٔ «آرشیو تصمیم»:** این یکی از دقیق‌ترین توصیه‌های کل راهنمای گوگل است. سند طراحی، «حقیقتِ» سیستم نیست. اگر آن را به‌عنوان مستنداتِ فعلی بخوانید، دربارهٔ چیزی که دیگر وجود ندارد اطلاعات غلط می‌دهید. آن را به‌عنوان **تاریخچهٔ تصمیم** بخوانید.
>
> این دقیقاً همان چیزی است که مقالهٔ [*Which documentation for software maintenance?*](https://link.springer.com/article/10.1007/BF03194494) به‌عنوان مهم‌ترین نیاز نگهدارنده شناسایی کرد: مستنداتِ **طراحی و تصمیم**، نه مستنداتِ کد.

---

## ۶. تکرار، شیطان است

> Do not write your own guide to a common Google technology or process. Link to it instead. If the guide doesn't exist or it's badly out of date, submit your updates to the appropriate directory or create a package-level README.md. **Take ownership and don't be shy**: Other teams will usually welcome your contributions.

**راهنمای خودت را برای یک فناوری یا فرآیند رایج ننویس. به‌جایش لینک بده.** اگر راهنما وجود ندارد یا به‌شدت منسوخ است، به‌روزرسانی‌هایت را به پوشهٔ مربوطه ارسال کن یا یک `README.md` در سطح پکیج بساز.

**مالکیت را بپذیر و خجالت نکش** — تیم‌های دیگر معمولاً از مشارکت شما استقبال می‌کنند.

> **دلیل منطقی این اصل:** هر بار که یک تیم راهنمای خودش را برای یک ابزار مشترک می‌نویسد، یک نسخهٔ **منسوخ** جدید متولد می‌شود. تکرار، «تضمین کیفیت» نیست؛ **دشمن** آن است. برای مستندات، تکرار یعنی ضریب شکست.
>
> **این با [اصل ۱ (کمترین مستندات قابل‌قبول)](https://google.github.io/styleguide/docguide/best_practices.html) کاملاً هم‌راستاست:** حجم زیاد، کیفیت را کاهش می‌دهد.

---

## سلسله‌مراتب کامل مستندات مهندسی

| # | سطح | نقش | اصل راهنما |
|---|---|---|---|
| ۱ | **نام‌های معنادار** | کد اطلاعات را خودش منتقل کند | جدی‌ترین سرمایه‌گذاری |
| ۲ | **کامنت درون‌خطی** | «چرا» — چیزی که کد نمی‌تواند بگوید | فقط «چرا»، نه «چه» |
| ۳a | **مستندات API متد** | قرارداد رفتار | «این یک چکش است» |
| ۳b | **مستندات کلاس/ماژول** | نمای کلی + مثال | ساده‌ترین مثال اول |
| ۴ | **README.md** | جهت‌دهی: کجا چیست | پاسخ به «کجا» |
| ۵ | **docs/** | چگونه: شروع، تست، دیباگ، انتشار | چهار سؤال ثابت |
| ۶ | **سند طراحی / PRD** | آرشیو تصمیم‌ها | تاریخچه، نه حقیقتِ فعلی |
| ۷ | **مستندات بیرونی** | جدا از کد | حتماً لینک‌شده از README |

---

## فلسفهٔ پشت راهنما

راهنمای گوگل بر سه اصل بنا شده که در سراسر متن تکرار می‌شوند:

### ۱. مستندات برای انسان‌ها

> **write for humans first, computers second**

اول برای انسان، بعد برای کامپیوتر. هر تصمیمی در این راهنما از همین یک جمله مشتق می‌شود.

### ۲. کمتر، تازه‌تر، دقیق‌تر

> **Docs work best when they are alive but frequently trimmed, like a bonsai tree**

حجم کم، تازگی زیاد. هر سه اصل دیگر (حذف مرده‌ها، خوب بهتر از کامل، تکرار شیطان است) از همین نتیجه می‌شوند.

### ۳. مستندات، هم‌زمان با کد

> **Change your documentation in the same CL as the code change**

هم‌زمانی، سازوکاری است که اصل دوم را اجرایی می‌کند. بدون هم‌زمانی، «هرس کردن» تبدیل به «بازسازی» می‌شود — که گران‌ترین حالت ممکن است.

---

## یادداشت شخصی

> **اهمیت این راهنما:** این تنها سند از این مجموعه است که **نوشتهٔ یک سازمان بزرگ و موفق برای استفادهٔ روزمرهٔ کارکنانش** است. سایر منابع نظریه‌اند؛ این یکی **دستورالعمل** است. و به همین دلیل، بیشترین ترجمهٔ عملی را دارد.
>
> **۱) مهم‌ترین ایدهٔ کل راهنما در یک جمله: «کم، اما دقیق».** استعارهٔ بونسای، بهترین جمله‌ای است که در کل ادبیات مستندسازی دربارهٔ حذف نوشته شده. ما وسوسه می‌شویم چیزی را حذف نکنیم چون «شاید به درد کسی بخورد». اما گوگل می‌گوید: آن سند، ناامیدی و تنبلی می‌آفریند — یعنی **ضربهٔ روانی** می‌زند، نه صرفاً اتلاف وقت.
>
> **۲) استعارهٔ «چکش» (hammer) را در عمل استفاده کرده‌ام.** «این یک چکش است. از آن برای کوبدن میخ استفاده می‌کنی.» این جمله، معیارِ نوشتن docstring را از حالت توضیح‌دادن به حالت **نقش‌دادن** تغییر می‌دهد. جای `recalculate()` بنویس `recalculateRateFromTieredPricingTable()` — ۰۰. این یک تغییر، نیمی از مشکل مستندات API را حل می‌کند، بدون اینکه یک خط هم سند اضافه کنی.
>
> **۳) اصل «کامنت = چرا، نه چه» را جدی گرفته‌ام و نتیجه‌اش ملموس بود.** کامنت‌های `// increment i` را در یک پروژه حذف کردم. بلافاصله فهمیدم که آنجا کامنت باید می‌گفت «چرا در اینجا، و نه در جای دیگر» — که جای خالی بود. یعنی بخشی از کد، **راز پشت‌ش را از دست داده بود**. حذف مستندات بی‌مورد، یک نوع «مستندسازی معکوس» هم هست: نشان می‌دهد کجا باید مستند نوشته شود.
>
> **۴) جمله‌ای که بیشترین تکرار را در ذهن من دارد:** «تکرار، شیطان است.» این اصل، پس از خواندن راهنمای گوگل، به ملاکِ شخصی من تبدیل شد. قبلاً فکر می‌کردم داشتن نسخهٔ محلی از یک راهنما، هوشمندی است. حالا فکر می‌کنم **قرضی** است. اگر راهنمای مشترکی کم‌کم می‌شود، من **می‌سازمش** — این کار هم کار را حل می‌کند و هم سهمم را در کیفیت وارد می‌کند. این همان چیزی است که [*Docs Like Code*](https://www.docslikecode.com/) دربارهٔ همکاری و مشارکت می‌گوید، اما از زاویهٔ «دوپارگیِ مستندات».
>
> **۵) جایگاهش در این مجموعه:** این راهنما «اصول پایه» است. [مقالهٔ Lethbridge et al.](https://ieeexplore.ieee.org/document/1241364) به شما می‌گوید **چرا** مستندات از کار می‌افتند (ظرفیت، نه نگرش). [مقالهٔ de Souza و همکاران](https://link.springer.com/article/10.1007/BF03194494) می‌گوید **چه چیزی** مهم‌تر است (تصمیم‌ها، نه کد). گوگل می‌گوید **چطور** رفتار کنیم (کم، تازه، هم‌زمان با کد). و این سه با هم، **اجزای تشکیل‌دهندهٔ [Diátaxis](https://diataxis.fr/)** را می‌سازند: نیاز (مقالهٔ دوم)، شکل (گوگل)، و چهار ربع (Diátaxis).
>
> **پیشنهاد من:** این راهنما کوتاه‌ترین و کاربردی‌ترین منبع کل مجموعه است. اگر فقط وقت خواندن یک صفحه را دارید، همین را بخوانید. هفت اصل آن، چک‌لیستِ عملیِ مستندسازی است که هر هفته می‌توانید با آن تیمتان را بسنجید.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۹/۳۰
**منبع اصلی:** [Google Developer Documentation Style Guide - Documentation Best Practices](https://google.github.io/styleguide/docguide/best_practices.html)
