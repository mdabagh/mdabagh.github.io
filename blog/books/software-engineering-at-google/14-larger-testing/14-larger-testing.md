> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۳۰۳
> Example 13-15. State testing
> @Test public void sortNumbers() {
> NumberSorter numberSorter = new NumberSorter(quicksort, bubbleSort);
> // Call the system under test.
> List sortedList = numberSorter.sortNumbers(newList(3, 1, 2));
> // Validate that the returned list is sorted. It doesn’t matter which
> // sorting algorithm is used, as long as the right result was returned.
> assertThat(sortedList).isEqualTo(newList(1, 2, 3));
> }
> Example 13-16 illustrates a similar test scenario but instead uses interaction testing.
> Note how it’s impossible for this test to determine that the numbers are actually sor‐
> ted, because the test doubles don’t know how to sort the numbers—all it can tell you
> is that the system under test tried to sort the numbers.
> Example 13-16. Interaction testing
> @Test public void sortNumbers_quicksortIsUsed() {
> // Pass in test doubles that were created by a mocking framework.
> NumberSorter numberSorter =
> new NumberSorter(mockQuicksort, mockBubbleSort);
> // Call the system under test.
> numberSorter.sortNumbers(newList(3, 1, 2));
> // Validate that numberSorter.sortNumbers() used quicksort. The test
> // will fail if mockQuicksort.sort() is never called (e.g., if
> // mockBubbleSort is used) or if it’s called with the wrong arguments.
> verify(mockQuicksort).sort(newList(3, 1, 2));
> }
> At Google, we’ve found that emphasizing state testing is more scalable; it reduces test
> brittleness, making it easier to change and maintain code over time.
> The primary issue with interaction testing is that it can’t tell you that the system
> under test is working properly; it can only validate that certain functions are called as
> expected. It requires you to make an assumption about the behavior of the code; for
> example, “If database.save(item) is called, we assume the item will be saved to the
> database.” State testing is preferred because it actually validates this assumption (such
> as by saving an item to a database and then querying the database to validate that the
> item exists).
> Another downside of interaction testing is that it utilizes implementation details of
> the system under test—to validate that a function was called, you are exposing to the
> test that the system under test calls this function. Similar to stubbing, this extra code
> makes tests brittle because it leaks implementation details of your production code
> into tests. Some people at Google jokingly refer to tests that overuse interaction
> 276
> |
> Chapter 13: Test Doubles

**تست وضعیت (State Testing) در مقابل تست تعاملی (Interaction Testing)**

Example 13-15 تست وضعیت را نشان می‌دهد. در این رویکرد، روی رفتار خروجی سیستم تحت تست تمرکز می‌شود. لیست ورودی به سیستم داده می‌شود و سپس بررسی می‌شود که آیا لیست خروجی مرتب شده است یا خیر. مهم نیست از چه الگوریتم مرتب‌سازی استفاده شده، تا زمانی که نتیجه صحیح برگردانده شود.

Example 13-16 یک سناریوی تست مشابه را نشان می‌دهد اما به جای آن از interaction testing (تست تعاملی) استفاده می‌کند. توجه کنید که چگونه این تست نمی‌تواند تعیین کند که اعداد واقعاً مرتب شده‌اند، زیرا test doubleها نمی‌دانند چگونه اعداد را مرتب کنند — تنها چیزی که می‌تواند به شما بگوید این است که سیستم تحت تست سعی کرده اعداد را مرتب کند.

در گوگل، دریافته‌ایم که تأکید بر تست وضعیت مقیاس‌پذیرتر است؛ شکنندگی تست‌ها را کاهش می‌دهد و تغییر و نگهداری کد را در طول زمان آسان‌تر می‌کند.

مشکل اصلی interaction testing این است که نمی‌تواند به شما بگوید سیستم تحت تست به درستی کار می‌کند؛ فقط می‌تواند تأیید کند که توابع خاصی مطابق انتظار فراخوانی شده‌اند. این رویکرد نیاز دارد شما درباره رفتار کد فرضیه بسازید؛ به عنوان مثال، "اگر database.save(item) فراخوانی شود، فرض می‌کنیم آیتم در پایگاه داده ذخیره خواهد شد." تست وضعیت ترجیح داده می‌شود زیرا واقعاً این فرضیه را تأیید می‌کند (مانند ذخیره یک آیتم در پایگاه داده و سپس پرس‌وجو از پایگاه داده برای تأیید وجود آیتم).

یکی دیگر از معایب interaction testing این است که از جزئیات پیاده‌سازی سیستم تحت تست استفاده می‌کند — برای تأیید اینکه یک تابع فراخوانی شده، شما در معرض تست قرار می‌دهید که سیستم تحت تست این تابع را فراخوانی می‌کند. مشابه stubbing، این کد اضافی باعث شکننده شدن تست‌ها می‌شود زیرا جزئیات پیاده‌سازی کد production شما را به تست‌ها نشت می‌دهد. برخی از افراد در گوگل به طنز به تست‌هایی که بیش از حد از interaction testing استفاده می‌کنند


![Section](images/page001-303.png)

![Section](images/page002-304.png)

![Section](images/page003-305.png)

![Section](images/page004-306.png)

![Section](images/page005-307.png)

---

###### 📄 صفحه ۳۰۸
> CHAPTER 14
> Larger Testing
> Written by Joseph Graves
> Edited by Tom Manshreck
> In previous chapters, we have recounted how a testing culture was established at
> Google and how small unit tests became a fundamental part of the developer work‐
> flow. But what about other kinds of tests? It turns out that Google does indeed use
> many larger tests, and these comprise a significant part of the risk mitigation strategy
> necessary for healthy software engineering. But these tests present additional chal‐
> lenges to ensure that they are valuable assets and not resource sinks. In this chapter,
> we'll discuss what we mean by "larger tests," when we execute them, and best practi‐
> ces for keeping them effective.
> What Are Larger Tests?
> As mentioned previously, Google has specific notions of test size. Small tests are
> restricted to one thread, one process, one machine. Larger tests do not have the same
> restrictions. But Google also has notions of test scope. A unit test necessarily is of
> smaller scope than an integration test. And the largest-scoped tests (sometimes called
> end-to-end or system tests) typically involve several real dependencies and fewer test
> doubles.
> Larger tests are many things that small tests are not. They are not bound by the same
> constraints; thus, they can exhibit the following characteristics:
> • They may be slow. Our large tests have a default timeout of 15 minutes or 1 hour,
> but we also have tests that run for multiple hours or even days.
> • They may be nonhermetic. Large tests may share resources with other tests and
> traffic.
> 281

**فصل ۱۴: تست‌های بزرگتر**

**نویسنده: Joseph Graves**
**ویراستار: Tom Manshreck**

در فصل‌های قبلی، توضیح دادیم که چگونه فرهنگ تست در گوگل ایجاد شد و چگونه تست‌های کوچک unit به بخش اساسی گردش کار توسعه‌دهنده تبدیل شدند. اما درباره سایر انواع تست‌ها چطور؟ مشخص است که گوگل واقعاً از تست‌های بزرگتر زیادی استفاده می‌کند و این تست‌ها بخش قابل توجهی از استراتژی کاهش ریسک (Risk Mitigation Strategy) لازم برای مهندسی نرم‌افزار سالم را تشکیل می‌دهند. اما این تست‌ها چالش‌های اضافی ایجاد می‌کنند تا اطمینان حاصل شود که دارایی‌های ارزشمند هستند و نه منابع مصرف‌کننده (Resource Sinks). در این فصل، درباره معنای "تست‌های بزرگتر" بحث خواهیم کرد، چه زمانی آن‌ها را اجرا می‌کنیم و بهترین شیوه‌ها برای حفظ اثربخشی آن‌ها.

**تست‌های بزرگتر چیست؟**

همان‌طور که قبلاً ذکر شد، گوگل مفاهیم خاصی برای اندازه تست دارد. تست‌های کوچک (Small Tests) به یک thread، یک process و یک machine محدود هستند. تست‌های بزرگتر چنین محدودیت‌هایی ندارند. اما گوگل همچنین مفاهیمی برای scope تست دارد. یک تست unit لزوماً scope کوچکتری نسبت به تست integration دارد. و تست‌های با بزرگترین scope (گاهی اوقات به نام end-to-end tests یا system tests شناخته می‌شوند) معمولاً شامل چندین وابستگی واقعی و test double کمتری هستند.

تست‌های بزرگتر چیزهای زیادی هستند که تست‌های کوچک نیستند. آن‌ها توسط محدودیت‌های یکسانی محدود نشده‌اند؛ بنابراین، می‌توانند ویژگی‌های زیر را نشان دهند:
- ممکن است کند باشند. تست‌های بزرگ ما timeout پیش‌فرض ۱۵ دقیقه یا ۱ ساعت دارند، اما تست‌هایی نیز داریم که چندین ساعت یا حتی روزها اجرا می‌شوند.
- ممکن است nonhermetic باشند. تست‌های بزرگ ممکن است منابع را با سایر تست‌ها و ترافیک به اشتراک بگذارند.


![Section](images/page006-308.png)

![Section](images/page007-309.png)

![Section](images/page008-310-img1.png)

![Section](images/page009-311.png)

![Section](images/page010-312.png)

---

###### 📄 صفحه ۳۱۳
> single approach to Nooglers (new Googlers) or even more experienced engineers,
> which both perpetuates the situation and also leads to a lack of understanding about
> the motivations of such tests.
> Larger Tests at Google
> When we discussed the history of testing at Google earlier (see Chapter 11), we men‐
> tioned how Google Web Server (GWS) mandated automated tests in 2003 and how
> this was a watershed moment. However, we actually had automated tests in use before
> this point, but a common practice was using automated large and enormous tests. For
> example, AdWords created an end-to-end test back in 2001 to validate product sce‐
> narios. Similarly, in 2002, Search wrote a similar "regression test" for its indexing
> code, and AdSense (which had not even publicly launched yet) created its variation
> on the AdWords test.
> Other "larger" testing patterns also existed circa 2002. The Google search frontend
> relied heavily on manual QA—manual versions of end-to-end test scenarios. And
> Gmail got its version of a "local demo" environment—a script to bring up an end-to-
> end Gmail environment locally with some generated test users and mail data for local
> manual testing.
> When C/J Build (our first continuous build framework) launched, it did not distin‐
> guish between unit tests and other tests, but there were two critical developments that
> led to a split. First, Google focused on unit tests because we wanted to encourage the
> testing pyramid and to ensure the vast majority of written tests were unit tests. Sec‐
> ond, when TAP replaced C/J Build as our formal continuous build system, it was only
> able to do so for tests that met TAP's eligibility requirements: hermetic tests buildable
> at a single change that could run on our build/test cluster within a maximum time
> limit. Although most unit tests satisfied this requirement, larger tests mostly did not.
> However, this did not stop the need for other kinds of tests, and they have continued
> to fill the coverage gaps. C/J Build even stuck around for years specifically to handle
> these kinds of tests until newer systems replaced it.
> Larger Tests and Time
> Throughout this book, we have looked at the influence of time on software engineer‐
> ing, because Google has built software running for more than 20 years. How are
> larger tests influenced by the time dimension? We know that certain activities make
> more sense the longer the expected lifespan of code, and testing of various forms is an
> activity that makes sense at all levels, but the test types that are appropriate change
> over the expected lifetime of code.
> As we pointed out before, unit tests begin to make sense for software with an
> expected lifespan from hours on up. At the minutes level (for small scripts), manual
> 286
> |
> Chapter 14: Larger Testing

**تست‌های بزرگتر در گوگل**

زمانی که قبلاً درباره تاریخچه تست در گوگل بحث کردیم (فصل ۱۱ را ببینید)، توضیح دادیم که چگونه Google Web Server (GWS) در سال ۲۰۰۳ تست‌های خودکار را اجباری کرد و چگونه این یک لحظه تعیین‌کننده بود. با این حال، ما در واقع قبل از این زمان نیز از تست‌های خودکار استفاده می‌کردیم، اما یک روی رایج رایج استفاده از تست‌های خودکار بزرگ و عظیم بود. به عنوان مثال، AdWords در سال ۲۰۰۱ یک تست end-to-end برای تأیید سناریوهای محصول ایجاد کرد. به طور مشابه، در سال ۲۰۰۲، Search یک "regression test" مشابه برای کد ایندکسینگ خود نوشت و AdSense (که حتی هنوز به صورت عمومی راه‌اندازی نشده بود) نسخه خود از تست AdWords را ایجاد کرد.

سایر الگوهای تست "بزرگتر" نیز حدود سال ۲۰۰۲ وجود داشتند. Front-end جستجوی گوگل به شدت به QA دستی (手动 Quality Assurance) وابسته بود — نسخه‌های دستی سناریوهای تست end-to-end. و Gmail نسخه خود از محیط "local demo" را دریافت کرد — یک اسکریپت برای راه‌اندازی محیط end-to-end Gmail به صورت محلی با برخی کاربران تست و داده‌های پستی تولید شده برای تست دستی محلی.

وقتی C/J Build (اولین continuous build framework ما) راه‌اندازی شد، بین تست‌های unit و سایر تست‌ها تمایز قائل نشد، اما دو تحول منجر به جدایی شد. اول، گوگل روی تست‌های unit تمرکز کرد زیرا می‌خواستیم testing pyramid (هرم تست) را تشویق کنیم و اطمینان حاصل کنیم که اکثریت قاطع تست‌های نوشته شده، تست‌های unit باشند. دوم، وقتی TAP جایگزین C/J Build به عنوان سیستم continuous build رسمی ما شد، فقط برای تست‌هایی که شرایط واجد بودن TAP را برآورده می‌کردند، قادر به انجام این کار بود: تست‌های hermetic که در یک change قابل build باشند و بتوانند در cluster build/test ما در یک محدوده زمانی حداکثر اجرا شوند. اگرچه بیشتر تست‌های unit این شرط را برآورده می‌کردند، تست‌های بزرگتر عمدتاً چنین نبودند.

**تست‌های بزرگتر و زمان**

در سراسر این کتاب، تأثیر زمان بر مهندسی نرم‌افزار را بررسی کرده‌ایم، زیرا گوگل نرم‌افزاری ساخته که بیش از ۲۰ سال در حال اجراست. چگونه تست‌های بزرگتر تحت تأثیر بُعد زمان قرار می‌گیرند؟ می‌دانیم که فعالیت‌های خاصی با طولانی‌تر شدن عمر مفید مورد انتظار کد، معنادارتر می‌شوند و تست در اشکال مختلف فعالیتی است که در همه سطوح معنادار است، اما انواع تست مناسب با طول عمر مورد انتظار کد تغییر می‌کنند.

همان‌طور که قبلاً اشاره کردیم، تست‌های unit برای نرم‌افزاری با عمر مفید مورد اانتظار از چند ساعت به بالا شروع به معنا پیدا کردن می‌کنند. در سطح دقیقه‌ها (برای اسکریپت‌های کوچک)،


![Section](images/page011-313.png)

![Section](images/page012-314.png)

![Section](images/page013-315-img1.png)

![Section](images/page014-316-img1.png)

![Section](images/page015-317-img1.png)

---

###### 📄 صفحه ۳۱۸
> Single-machine SUT
> The system under test consists of one or more separate binaries (same as produc‐
> tion) and the test is its own binary. But everything runs on one machine. This is
> used for "medium" tests. Ideally, we use the production launch configuration of
> each binary when running those binaries locally for increased fidelity.
> Multimachine SUT
> The system under test is distributed across multiple machines (much like a pro‐
> duction cloud deployment). This is even higher fidelity than the single-machine
> SUT, but its use makes tests "large" size and the combination is susceptible to
> increased network and machine flakiness.
> Shared environments (staging and production)
> Instead of running a standalone SUT, the test just uses a shared environment.
> This has the lowest cost because these shared environments usually already exist,
> but the test might conflict with other simultaneous uses and one must wait for
> the code to be pushed to those environments. Production also increases the risk
> of end-user impact.
> Hybrids
> Some SUTs represent a mix: it might be possible to run some of the SUT but have
> it interact with a shared environment. Usually the thing being tested is explicitly
> run but its backends are shared. For a company as expansive as Google, it is prac‐
> tically impossible to run multiple copies of all of Google's interconnected serv‐
> ices, so some hybridization is required.
> The benefits of hermetic SUTs
> The SUT in a large test can be a major source of both unreliability and long turn‐
> around time. For example, an in-production test uses the actual production system
> deployment. As mentioned earlier, this is popular because there is no extra overhead
> cost for the environment, but production tests cannot be run until the code reaches
> that environment, which means those tests cannot themselves block the release of the
> code to that environment—the SUT is too late, essentially.
> The most common first alternative is to create a giant shared staging environment
> and to run tests there. This is usually done as part of some release promotion process,
> but it again limits test execution to only when the code is available. As an alternative,
> some teams will allow engineers to "reserve" time in the staging environment and to
> use that time window to deploy pending code and to run tests, but this does not scale
> with a growing number of engineers or a growing number of services, because the
> environment, its number of users, and the likelihood of user conflicts all quickly
> grow.
> Structure of a Large Test
> |
> 291

**ساختار SUT (سیستم تحت تست)**

**SUT تک machine**
سیستم تحت تست از یک یا چند binary جداگانه تشکیل شده (همانند production) و تست خودش یک binary مستقل است. اما همه چیز روی یک machine اجرا می‌شود. این برای تست‌های "متوسط" استفاده می‌شود. ایده‌آل این است که از پیکربندی launch production هر binary هنگام اجرای محلی آن‌ها برای fidelity (دقیق بودن) بیشتر استفاده شود.

**SUT چند machine**
سیستم تحت测试 در چندین machine توزیع شده (بسیار شبیه استقرار ابری production). این حتی fidelity بالاتری نسبت به SUT تک machine دارد، اما استفاده از آن تست‌ها را "بزرگ" می‌کند و ترکیب آن در معرض افزایش network flakiness (شکنندگی شبکه) و machine flakiness قرار دارد.

**محیط‌های مشترک (staging و production)**
به جای اجرای یک SUT مستقل، تست فقط از یک محیط مشترک استفاده می‌کند. این کمترین هزینه را دارد زیرا این محیط‌های مشترک معمولاً از قبل وجود دارند، اما ممکن است تست با سایر استفاده‌های همزمان تداخل داشته باشد و باید منتظر ماند که کد به آن محیط‌ها push شود. Production همچنین خطر تأثیر بر کاربر نهایی را افزایش می‌دهد.

**هیبریدها**
برخی SUTها ترکیبی هستند: ممکن است بتوان بخشی از SUT را اجرا کرد اما آن را با یک محیط مشترک تعامل داد. معمولاً چیزی که تست می‌شود به صورت صریح اجرا می‌شود اما backendهای آن مشترک هستند. برای شرکتی به وسعت گوگل، عملاً غیرممکن است چندین نسخه از تمام سرویس‌های به هم پیوسته گوگل اجرا شود، بنابراین ترکیب‌بندی (Hybridization) لازم است.

**مزایای SUTهای hermetic**
SUT در یک تست بزرگ می‌تواند منبع اصلی عدم قابلیت اطمینان و زمان turn-around طولانی باشد. به عنوان مثال، یک test in-production از استقرار واقعی سیستم production استفاده می‌کند. همان‌طور که قبلاً ذکر شد، این روش محبوب است زیرا هزینه overhead اضافی برای محیط وجود ندارد، اما تست‌های production تا زمانی که کد به آن محیط نرسد، قابل اجرا نیستند — یعنی SUT اساساً دیر است.

رایج‌ترین جایگزین اولیه ایجاد یک محیط staging مشترک عظیم و اجرای تست‌ها در آنجا است. این معمولاً به عنوان بخشی از فرآیند release promotion انجام می‌شود، اما دوباره اجرای تست را فقط به زمانی محدود می‌کند که کد در دسترس باشد. به عنوان جایگزین، برخی تیم‌ها به مهندسان اجازه می‌دهند "زمانی" را در محیط staging رزرو کنند و از آن پنجره زمانی برای استقرار کد در انتظار و اجرای تست‌ها استفاده کنند، اما این با تعداد فزاینده مهندسان یا تعداد فزاینده سرویس‌ها مقیاس نمی‌یابد، زیرا محیط، تعداد کاربران آن و احتمال تداخل کاربران همگی به سرعت رشد می‌کنند.


![Section](images/page016-318-img1.png)

![Section](images/page017-319.png)

![Section](images/page018-320.png)

![Section](images/page019-321-img1.png)

![Section](images/page020-322.png)

---

###### 📄 صفحه ۳۲۳
> A/B comparison (differential)
> Instead of defining explicit assertions, A/B testing involves running two copies of
> the SUT, sending the same data, and comparing the output. The intended behav‐
> ior is not explicitly defined: a human must manually go through the differences
> to ensure any changes are intended.
> Types of Larger Tests
> We can now combine these different approaches to the SUT, data, and assertions to
> create different kinds of large tests. Each test then has different properties as to which
> risks it mitigates; how much toil is required to write, maintain, and debug it; and how
> much it costs in terms of resources to run.
> What follows is a list of different kinds of large tests that we use at Google, how they
> are composed, what purpose they serve, and what their limitations are:
> • Functional testing of one or more binaries
> • Browser and device testing
> • Performance, load, and stress testing
> • Deployment configuration testing
> • Exploratory testing
> • A/B diff (regression) testing
> • User acceptance testing (UAT)
> • Probers and canary analysis
> • Disaster recovery and chaos engineering
> • User evaluation
> Given such a wide number of combinations and thus a wide range of tests, how do we
> manage what to do and when? Part of designing software is drafting the test plan, and
> a key part of the test plan is a strategic outline of what types of testing are needed and
> how much of each. This test strategy identifies the primary risk vectors and the nec‐
> essary testing approaches to mitigate those risk vectors.
> At Google, we have a specialized engineering role of "Test Engineer," and one of the
> things we look for in a good test engineer is the ability to outline a test strategy for
> our products.
> 296
> |
> Chapter 14: Larger Testing

**مقایسه A/B (دیفرانسیل)**

به جای تعریف assertion‌های صریح، تست A/B شامل اجرای دو نسخه از SUT، ارسال داده‌های یکسان و مقایسه خروجی‌ها است. رفتار مورد نظر به صورت صریح تعریف نشده: یک انسان باید به صورت دستی تفاوت‌ها را بررسی کند تا اطمینان حاصل شود هر تغییری مورد نظر است.

**انواع تست‌های بزرگتر**

اکنون می‌توانیم این رویکردهای مختلف به SUT، داده‌ها و assertionها را ترکیب کنیم تا انواع مختلف تست‌های بزرگ را ایجاد کنیم. هر تست سپس ویژگی‌های متفاوتی از نظر اینکه چه ریسک‌هایی را کاهش می‌دهد؛ چقدر زحمت برای نوشتن، نگهداری و debug کردن لازم است؛ و چقدر از نظر منابع هزینه اجرا دارد، خواهد داشت.

فهرست زیر انواع مختلف تست‌های بزرگی است که در گوگل استفاده می‌کنیم، نحوه ترکیب آن‌ها، هدفشان و محدودیت‌هایشان:
- تست عملکردی (Functional Testing) یک یا چند binary
- تست مرورگر و دستگاه
- تست عملکرد (Performance)، بار (Load) و استرس (Stress)
- تست پیکربندی استقرار (Deployment Configuration)
- تست اکتشافی (Exploratory Testing)
- تست A/B diff (بازگشتی)
- تست پذیرش کاربر (User Acceptance Testing - UAT)
- Probers و canary analysis (تحلیل canary)
- بازیابی از فاجعه (Discovery Recovery) و مهندسی آشوب (Chaos Engineering)
- ارزیابی کاربر

با این تعداد زیاد ترکیبات و در نتیجه طیف وسیعی از تست‌ها، چگونه مدیریت می‌کنیم چه کاری انجام دهیم و چه زمانی؟ بخشی از طراحی نرم‌افزار، تهیه plan تست است و بخش کلیدی plan تست، یک طرح استراتژیک از انواع تست مورد نیاز و مقدار هر کدام است. این استراتژی تست، بردارهای ریسک اصلی و رویکردهای تست لازم برای کاهش آن بردارهای ریسک را شناسایی می‌کند.

در گوگل، نقش مهندسی تخصصی "Test Engineer" داریم و یکی از چیزهایی که در یک test engineer خوب جستجو می‌کنیم، توانایی ترسیم یک استراتژی تست برای محصولاتمان است.


![Section](images/page021-323.png)

![Section](images/page022-324.png)

![Section](images/page023-325.png)

![Section](images/page024-326.png)

![Section](images/page025-327.png)

![Section](images/page026-328.png)

![Section](images/page027-329.png)

![Section](images/page028-330.png)

---