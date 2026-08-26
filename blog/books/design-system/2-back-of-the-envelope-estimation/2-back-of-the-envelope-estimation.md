> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---

###### 📄 صفحه ۳۴

> **CHAPTER 2:** In a system design interview, sometimes you are asked to estimate system capacity or performance requirements using a back-of-the-envelope estimation. According to Jeff Dean, Google Senior Fellow, "back-of-the-envelope calculations are estimates you create using a combination of thought experiments and common performance numbers to get a good feel for which designs will meet your requirements" [1].
> You need to have a good sense of scalability basics to effectively carry out back-of-the-envelope estimation. The following concepts should be well understood: power of two [2], latency numbers every programmer should know, and availability numbers.

**فصل ۲:** در مصاحبه‌های طراحی سیستم، گاهی از شما خواسته می‌شود ظرفیت سیستم یا نیازمندی‌های عملکردی را با استفاده از **تخمین پشت پاکتی (Back-of-the-Envelope Estimation)** تخمین بزنید. به گفته **جف دین (Jeff Dean)**، همکار ارشد گوگل: «محاسبات پشت پاکتی تخمین‌هایی هستند که با ترکیبی از آزمایش‌های فکری و اعداد عملکردی رایج ایجاد می‌شوند تا درک خوبی از اینکه کدام طراحی‌ها نیازهای شما را برآورده می‌کنند، به دست آورید» [۱].

برای انجام مؤثر تخمین پشت پاکتی، باید درک خوبی از مفاهیم پایه‌ای **مقیاس‌پذیری (Scalability)** داشته باشید. مفاهیم زیر باید به‌خوبی درک شوند: **توان‌های دو (Power of Two)** [۲]، **اعداد Latency که هر برنامه‌نویسی باید بداند**، و **اعداد Availability**.

---

###### 📄 صفحه ۳۵

> **Power of two:** Although data volume can become enormous when dealing with distributed systems, calculation all boils down to the basics. To obtain correct calculations, it is critical to know the data volume unit using the power of 2. A byte is a sequence of 8 bits. An ASCII character uses one byte of memory (8 bits). Below is a table explaining the data volume unit (Table 2-1).

### توان‌های دو (Power of Two)

اگرچه در سیستم‌های توزیع‌شده حجم داده‌ها می‌تواند بسیار عظیم شود، اما محاسبات در نهایت به مفاهیم پایه‌ای بازمی‌گردند. برای انجام محاسبات صحیح، دانستن واحدهای حجم داده بر اساس **توان‌های دو** ضروری است.

یک **بایت (Byte)** شامل ۸ بیت است. هر کاراکتر ASCII از یک بایت حافظه (۸ بیت) استفاده می‌کند. جدول زیر واحدهای حجم داده را توضیح می‌دهد (جدول ۲-۱).

---

###### 📄 صفحه ۳۶

> **Latency numbers every programmer should know:** Dr. Dean from Google reveals the length of typical computer operations in 2010 [1]. Some numbers are outdated as computers become faster and more powerful. However, those numbers should still be able to give us an idea of the fastness and slowness of different computer operations.
>
> Notes:
> ns = nanosecond, µs = microsecond, ms = millisecond
> 1 ns = 10^-9 seconds
> 1 µs = 10^-6 seconds = 1,000 ns
> 1 ms = 10^-3 seconds = 1,000 µs = 1,000,000 ns

### اعداد Latency که هر برنامه‌نویسی باید بداند

دکتر دین از گوگل در سال ۲۰۱۰ مدت زمان عملیات‌های رایج کامپیوتری را منتشر کرد [۱]. برخی از این اعداد با توجه به سریع‌تر و قوی‌تر شدن کامپیوترها قدیمی شده‌اند، اما همچنان می‌توانند درک خوبی از سرعت و کندی عملیات‌های مختلف کامپیوتری به ما بدهند.

**یادداشت‌ها:**
- ns = نانوثانیه (۱۰⁻⁹ ثانیه)
- µs = میکروثانیه (۱۰⁻۶ ثانیه = ۱,۰۰۰ نانوثانیه)
- ms = میلی‌ثانیه (۱۰⁻³ ثانیه = ۱,۰۰۰ میکروثانیه = ۱,۰۰۰,۰۰۰ نانوثانیه)

---

###### 📄 صفحه ۳۷

> A Google software engineer built a tool to visualize Dr. Dean's numbers. The tool also takes the time factor into consideration. Figures 2-1 shows the visualized latency numbers as of 2020 (source of figures: reference material [3]).
> By analyzing the numbers in Figure 2-1, we get the following conclusions:
> • Memory is fast but the disk is slow.
> • Avoid disk seeks if possible.
> • Simple compression algorithms are fast.
> • Compress data before sending it over the internet if possible.
> • Data centers are usually in different regions, and it takes time to send data between them.

یک مهندس نرم‌افزار گوگل ابزاری برای نمایش بصری اعداد دکتر دین ساخت. این ابزار عامل زمان را نیز در نظر می‌گیرد. شکل ۲-۱ اعداد Latency را تا سال ۲۰۲۰ نمایش می‌دهد (منبع تصاویر: مرجع شماره [۳]).

با تحلیل اعداد در شکل ۲-۱، به نتایج زیر می‌رسیم:

- **حافظه (Memory) سریع است اما دیسک کند است.**
- تا جایی که ممکن است از **Disk Seek** اجتناب کنید.
- **الگوریتم‌های فشرده‌سازی ساده سریع هستند.**
- در صورت امکان، داده‌ها را قبل از ارسال از طریق اینترنت فشرده کنید.
- **مراکز داده معمولاً در مناطق جغرافیایی مختلفی قرار دارند** و ارسال داده بین آن‌ها زمان‌بر است.

> ***یادداشت شخصی***
>
> 🔗 **ابزار تعاملی نمایش اعداد Latency:** [Interactive Latency Numbers](https://colin-scott.github.io/personal_website/research/interactive_latency.html)
>
> این ابزار تعاملی توسط Colin Scott ساخته شده و اعداد Jeff Dean را به صورت بصری و مقیاس‌پذیر نمایش می‌دهد. می‌توانید روی هر باکس کلیک کنید تا جزئیات و مقایسه با سخت‌افزارهای مختلف را ببینید.

---

###### 📄 صفحه ۳۸

> **Availability numbers:** High availability is the ability of a system to be continuously operational for a desirably long period of time. High availability is measured as a percentage, with 100% means a service that has 0 downtime. Most services fall between 99% and 100%.
>
> A service level agreement (SLA) is a commonly used term for service providers. This is an agreement between you (the service provider) and your customer, and this agreement formally defines the level of uptime your service will deliver. Cloud providers Amazon [4], Google [5] and Microsoft [6] set their SLAs at 99.9% or above. Uptime is traditionally measured in nines. The more the nines, the better. As shown in Table 2-3, the number of nines correlate to the expected system downtime.

### اعداد Availability

**در‌دسترس‌بودن بالا (High Availability)** توانایی یک سیستم برای عملکرد مستمر در بازه‌ی زمانی طولانی و مطلوب است. در‌دسترس‌بودن بالا به صورت درصد بیان می‌شود؛ ۱۰۰٪ به معنای سرویسی با **بدون زمان توقف (Zero Downtime)** است. بیشتر سرویس‌ها بین ۹۹٪ تا ۱۰۰٪ قرار دارند.

**قرارداد سطح سرویس (Service Level Agreement یا SLA)** اصطلاحی رایج برای ارائه‌دهندگان سرویس است. این قراردادی بین شما (ارائه‌دهنده سرویس) و مشتری شماست که به‌طور رسمی سطح uptime سرویس شما را تعریف می‌کند. ارائه‌دهندگان خدمات ابری مانند **آمازون [۴]**، **گوگل [۵]** و **مایکروسافت [۶]** SLA خود را روی ۹۹.۹٪ یا بالاتر تنظیم کرده‌اند.

زمان کارکرد (Uptime) به‌صورت سنتی با تعداد **«نُه» (Nines)** اندازه‌گیری می‌شود. هرچه تعداد نُه بیشتر باشد، وضعیت بهتر است. همان‌طور که در جدول ۲-۳ نشان داده شده، تعداد نُه‌ها با زمان توقف مورد انتظار سیستم همبستگی دارد.

---

###### 📄 صفحه ۳۹

> **Example: Estimate Twitter QPS and storage requirements**
> Please note the following numbers are for this exercise only as they are not real numbers from Twitter.
>
> Assumptions:
> • 300 million monthly active users.
> • 50% of users use Twitter daily.
> • Users post 2 tweets per day on average.
> • 10% of tweets contain media.
> • Data is stored for 5 years.
>
> Estimations:
> Query per second (QPS) estimate:
> • Daily active users (DAU) = 300 million * 50% = 150 million
> • Tweets QPS = 150 million * 2 tweets / 24 hour / 3600 seconds = ~3500
> • Peek QPS = 2 * QPS = ~7000
>
> We will only estimate media storage here.
> • Average tweet size:
>   • tweet_id: 64 bytes
>   • text: 140 bytes
>   • media: 1 MB
> • Media storage: 150 million * 2 * 10% * 1 MB = 30 TB per day
> • 5-year media storage: 30 TB * 365 * 5 = ~55 PB

### مثال: تخمین QPS و نیازمندی‌های ذخیره‌سازی توییتر

> **توجه:** اعداد زیر فقط برای این تمرین هستند و اعداد واقعی توییتر نیستند.

**فرضیات:**
- ۳۰۰ میلیون کاربر فعال ماهانه
- ۵۰٪ کاربران روزانه از توییتر استفاده می‌کنند
- کاربران به‌طور میانگین روزانه ۲ توییت ارسال می‌کنند
- ۱۰٪ توییت‌ها حاوی فایل‌های رسانه‌ای هستند
- داده‌ها به مدت ۵ سال نگهداری می‌شوند

**تخمین‌ها:**

**تخمین Query Per Second (QPS):**
- کاربران فعال روزانه (DAU) = ۳۰۰ میلیون × ۵۰٪ = ۱۵۰ میلیون
- QPS توییت‌ها = ۱۵۰ میلیون × ۲ توییت / ۲۴ ساعت / ۳۶۰۰ ثانیه = حدود ۳,۵۰۰
- QPS اوج (Peak) = ۲ × QPS = حدود ۷,۰۰۰

**تخمین ذخیره‌سازی رسانه:**
- اندازه متوسط توییت:
  - tweet_id: ۶۴ بایت
  - متن: ۱۴۰ بایت
  - رسانه: ۱ مگابایت
- ذخیره‌سازی رسانه: ۱۵۰ میلیون × ۲ × ۱۰٪ × ۱ مگابایت = ۳۰ ترابایت در روز
- ذخیره‌سازی ۵ ساله رسانه: ۳۰ ترابایت × ۳۶۵ × ۵ = حدود ۵۵ پتابایت

---

###### 📄 صفحه ۴۰

> **Tips:** Back-of-the-envelope estimation is all about the process. Solving the problem is more important than obtaining results. Interviewers may test your problem-solving skills. Here are a few tips to follow:
> • Rounding and Approximation. It is difficult to perform complicated math operations during the interview. For example, what is the result of "99987 / 9.1"? There is no need to spend valuable time to solve complicated math problems. Precision is not expected. Use round numbers and approximation to your advantage. The division question can be simplified as follows: "100,000 / 10".
> • Write down your assumptions. It is a good idea to write down your assumptions to be referenced later.
> • Label your units. When you write down "5", does it mean 5 KB or 5 MB? You might confuse yourself with this. Write down the units because "5 MB" helps to remove ambiguity.
> • Commonly asked back-of-the-envelope estimations: QPS, peak QPS, storage, cache, number of servers, etc. You can practice these calculations when preparing for an interview. Practice makes perfect.

### نکات تکمیلی

تخمین پشت پاکتی درباره **فرایند** است. حل مسئله مهم‌تر از رسیدن به نتیجه نهایی است. مصاحبه‌گر ممکن است مهارت‌های حل مسئله شما را بسنجد. در ادامه چند نکته مفید آورده شده است:

- **گرد کردن و تقریب (Rounding and Approximation):** انجام عملیات ریاضی پیچیده در طول مصاحبه دشوار است. برای مثال، حاصل تقسیم «۹۹۹۸۷ ÷ ۹.۱» چقدر است؟ نیازی نیست زمان ارزشمند خود را صرف حل مسائل ریاضی پیچیده کنید. دقت بالا مورد انتظار نیست. از اعداد رند و تقریب به نفع خود استفاده کنید. این تقسیم به‌سادگی به «۱۰ ÷ ۱۰۰,۰۰۰» تبدیل می‌شود.

- **فرضیات خود را یادداشت کنید:** نوشتن فرضیات برای مراجعه بعدی کار هوشمندانه‌ای است.

- **واحدها را مشخص کنید:** وقتی عدد «۵» را می‌نویسید، آیا منظور ۵ کیلوبایت است یا ۵ مگابایت؟ نوشتن واحدها (مانند «۵ مگابایت») ابهام را از بین می‌برد.

- **تخمین‌های رایج پشت پاکتی:** QPS، QPS اوج، ذخیره‌سازی، کش، تعداد سرورها و غیره. می‌توانید این محاسبات را هنگام آماده‌سازی برای مصاحبه تمرین کنید. **تمرین باعث کمال می‌شود.**

تبریک! تا اینجا پیش رفتید. حالا به خودتان یک آفرین بگویید. آفرین!

---

### مواد مرجع

[۱] J. Dean. Google Pro Tip: Use Back-Of-The-Envelope-Calculations To Choose The Best Design
[۲] System design primer: https://github.com/donnemartin/system-design-primer
[۳] Latency Numbers Every Programmer Should Know: https://colin-scott.github.io/personal_website/research/interactive_latency.html
[۴] Amazon Compute Service Level Agreement: https://aws.amazon.com/compute/sla/
[۵] Compute Engine Service Level Agreement (SLA): https://cloud.google.com/compute/sla
[۶] SLA summary for Azure services: https://azure.microsoft.com/en-us/support/legal/sla/summary/
