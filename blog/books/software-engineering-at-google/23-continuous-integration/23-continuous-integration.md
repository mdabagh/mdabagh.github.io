> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۵۰۱
> 14 This happens for many reasons: copy-and-paste from existing examples, committing changes that have been
> in development for some time, or simply reliance on old habits.
> 15 In actuality, this is the reasoning behind the original work on clang-format for C++.
> The change generation process should be as automated as possible so that the parent
> change can be updated as users backslide into old uses14 or textual merge conflicts
> occur in the changed code. Occasionally, for the rare case in which technical tools
> aren't able to generate the global change, we have sharded change generation across
> humans (see "Case Study: Operation RoseHub" on page 472). Although much more
> labor intensive than automatically generating changes, this allows global changes to
> happen much more quickly for time-sensitive applications.
> Keep in mind that we optimize for human readability of our codebase, so whatever
> tool generates changes, we want the resulting changes to look as much like human-
> generated changes as possible. This requirement leads to the necessity of style guides
> and automatic formatting tools (see Chapter 8).15
> Sharding and Submitting
> After a global change has been generated, the author then starts running Rosie. Rosie
> takes a large change and shards it based upon project boundaries and ownership
> rules into changes that can be submitted atomically. It then puts each individually
> sharded change through an independent test-mail-submit pipeline. Rosie can be a
> heavy user of other pieces of Google's developer infrastructure, so it caps the number
> of outstanding shards for any given LSC, runs at lower priority, and communicates
> with the rest of the infrastructure about how much load it is acceptable to generate on
> our shared testing infrastructure.
> We talk more about the specific test-mail-submit process for each shard below.
> Cattle Versus Pets
> We often use the "cattle and pets" analogy when referring to individual machines in a
> distributed computing environment, but the same principles can apply to changes
> within a codebase.
> At Google, as at most organizations, typical changes to the codebase are handcrafted
> by individual engineers working on specific features or bug fixes. Engineers might
> spend days or weeks working through the creation, testing, and review of a single
> change. They come to know the change intimately, and are proud when it is finally
> committed to the main repository. The creation of such a change is akin to owning
> and raising a favorite pet.
> 474
> |
> Chapter 22: Large-Scale Changes

**تولید تغییرات، خرد کردن و ارسال**

فرآیند تولید تغییرات باید تا حد ممکن خودکار باشد تا بتوان تغییر والد را به‌روزرسانی کرد زمانی که کاربران به استفاده‌های قدیمی بازمی‌گردند یا تعارضات ادغام متنی در کد تغییر یافته رخ می‌دهد. گاهی اوقات، در موارد نادری که ابزارهای فنی قادر به تولید تغییر جهانی نیستند، ما تولید تغییرات را بین انسان‌ها خرد کرده‌ایم (نگاه کنید به «مطالعه موردی: عملیات RoseHub» در صفحه ۴۷۲). اگرچه بسیار کاربراتر از تولید خودکار تغییرات است، این اجازه می‌دهد تغییرات جهانی بسیار سریع‌تر برای برنامه‌های حساس به زمان انجام شوند.

به یاد داشته باشید که ما برای خوانایی انسانی پایگاه کد خود بهینه‌سازی می‌کنیم، بنابراین هر ابزاری که تغییرات تولید می‌کند، می‌خواهیم تغییرات حاصل تا حد ممکن شبیه تغییرات تولید شده توسط انسان به نظر برسند. این الزام به ضرورت راهنماهای سبک و ابزارهای قالب‌بندی خودکار منجر می‌شود (نگاه کنید به فصل ۸).

**خرد کردن و ارسال (Sharding and Submitting)**

پس از تولید یک تغییر جهانی، نویسنده سپس Rosie را اجرا می‌کند. Rosie یک تغییر بزرگ را بر اساس مرزهای پروژه و قوانین مالکیت به تغییراتی خرد می‌کند که می‌توانند به صورت اتمیک ارسال شوند. سپس هر تغییر خرد شده جداگانه را از یک خط لوله مستقل test-mail-submit عبور می‌دهد. Rosie می‌تواند استفاده‌کننده سنگینی از بخش‌های دیگر زیرساخت توسعه‌دهنده گوگل باشد، بنابراین تعداد قطعه‌های خرد شده outstanding برای هر LSC مشخص را محدود می‌کند، با اولویت پایین‌تر اجرا می‌کند و با بقیه زیرساخت در مورد مقدار باری که تولید آن در زیرساخت تست مشترک ما قابل قبول است ارتباط برقرار می‌کند.

**گاوها در مقابل حیوانات خانگی (Cattle Versus Pets)**

ما اغلب از تمثیل «گاوها و حیوانات خانگی» هنگام اشاره به ماشین‌های جداگانه در یک محیط محاسبات توزیع‌شده استفاده می‌کنیم، اما همان اصول می‌توانند در مورد تغییرات در یک پایگاه کد اعمال شوند.

در گوگل، مانند اکثر سازمان‌ها، تغییرات معمولی در پایگاه کد توسط مهندسان جداگانه‌ای که روی ویژگی‌ها یا رفع باگ‌های خاصی کار می‌کنند با دست ساخته می‌شوند. مهندسان ممکن است روزها یا هفته‌ها صرف ایجاد، تست کردن و بررسی یک تغییر واحد کنند. آن‌ها با تغییر به طور نزدیک آشنا می‌شوند و زمانی که سرانجام در مخزن اصلی commit می‌شود به آن افتخار می‌کنند. ایجاد چنین تغییری شبیه به داشتن و بزرگ کردن حیوان خانگی مورد علاقه است.

![Section](images/page001-501.png)

![Section](images/page002-502.png)

![Section](images/page003-503.png)

![Section](images/page004-504.png)

---

###### 📄 صفحه ۵۰۵
> sistent, spatially and temporally. And all of this happens with only a few dozen
> engineers supporting tens of thousands of others.
> No matter the size of your organization, it's reasonable to think about how you would
> make these kinds of sweeping changes across your collection of source code. Whether
> by choice or by necessity, having this ability will allow greater flexibility as your orga‐
> nization scales while keeping your source code malleable over time.
> TL;DRs
> • An LSC process makes it possible to rethink the immutability of certain technical
> decisions.
> • Traditional models of refactoring break at large scales.
> • Making LSCs means making a habit of making LSCs.
> 478
> |
> Chapter 22: Large-Scale Changes

**نتیجه‌گیری Large-Scale Changes**

این امر در فضا و زمان سازگار است. و تمام اینها فقط با چند ده مهندس که از ده‌ها هزار مهندس دیگر پشتیبانی می‌کنند اتفاق می‌افتد.

صرف نظر از اندازه سازمان شما، منطقی است که در مورد نحوه انجام این نوع تغییرات گسترده در مجموعه کد منبع خود فکر کنید. چه به انتخاب و چه به اجبار، داشتن این قابلیت انعطاف‌پذیری بیشتری را هنگام مقیاس‌پذیری سازمان شما فراهم می‌کند و در عین حال کد منبع شما را در طول زمان انعطاف‌پذیر نگه می‌دارد.

**خلاصه‌ها (TL;DRs)**

• فرآیند LSC امکان بازنگری در تغییرناپذیری برخی تصمیمات فنی را فراهم می‌کند.
• مدل‌های سنتی بازآرایی (refactoring) در مقیاس‌های بزرگ شکست می‌خورند.
• ایجاد LSC به معنای ایجاد عادت ایجاد LSC است.

![Section](images/page005-505.png)

![Section](images/page006-506.png)

![Section](images/page007-507.png)

![Section](images/page008-508.png)

---

###### 📄 صفحه ۵۰۹
> • An incompatibility between our project and an upstream microservice depend‐
> ency, detected by a QA tester in our staging environment, when the upstream
> service deploys its latest changes
> • Bug reports by internal users who are opted in to a feature before external users
> • Bug or outage reports by external users or the press
> Canarying—or deploying to a small percentage of production first—can help mini‐
> mize issues that do make it to production, with a subset-of-production initial feed‐
> back loop preceding all-of-production. However, canarying can cause problems, too,
> particularly around compatibility between deployments when multiple versions are
> deployed at once. This is sometimes known as version skew, a state of a distributed
> system in which it contains multiple incompatible versions of code, data, and/or con‐
> figuration. Like many issues we look at in this book, version skew is another example
> of a challenging problem that can arise when trying to develop and manage software
> over time.
> Experiments and feature flags are extremely powerful feedback loops. They reduce
> deployment risk by isolating changes within modular components that can be
> dynamically toggled in production. Relying heavily on feature-flag-guarding is a
> common paradigm for Continuous Delivery, which we explore further in Chapter 24.
> Accessible and actionable feedback
> It's also important that feedback from CI be widely accessible. In addition to our open
> culture around code visibility, we feel similarly about our test reporting. We have a
> unified test reporting system in which anyone can easily look up a build or test run,
> including all logs (excluding user Personally Identifiable Information [PII]), whether
> for an individual engineer's local run or on an automated development or staging
> build.
> Along with logs, our test reporting system provides a detailed history of when build
> or test targets began to fail, including audits of where the build was cut at each run,
> where it was run, and by whom. We also have a system for flake classification, which
> uses statistics to classify flakes at a Google-wide level, so engineers don't need to fig‐
> ure this out for themselves to determine whether their change broke another project's
> test (if the test is flaky: probably not).
> Visibility into test history empowers engineers to share and collaborate on feedback,
> an essential requirement for disparate teams to diagnose and learn from integration
> failures between their systems. Similarly, bugs (e.g., tickets or issues) at Google are
> open with full comment history for all to see and learn from (with the exception,
> again, of customer PII).
> Finally, any feedback from CI tests should not just be accessible but actionable—easy
> to use to find and fix problems. We'll look at an example of improving user-
> 482
> |
> Chapter 23: Continuous Integration

** Canarying، بازخورد و قابلیت دسترسی**

canarying — یا استقرار ابتدا در درصد کوچکی از production — می‌تواند به کاهش مشکلاتی که وارد production می‌شوند کمک کند، با حلقه بازخورد اولیه زیرمجموعه‌ای از production قبل از کل production. با این حال، canarying هم می‌تواند مشکلاتی ایجاد کند، به ویژه در مورد سازگاری بین استقرارها زمانی که چندین نسخه همزمان مستقر می‌شوند. این گاهی اوقات به عنوان version skew شناخته می‌شود، وضعیتی از یک سیستم توزیع‌شده که حاوی چندین نسخه ناسازگار کد، داده و/یا پیکربندی است.

آزمایش‌ها و feature flagها حلقه‌های بازخورد بسیار قدرتمندی هستند. آن‌ها خطر استقرار را با ایزوله کردن تغییرات در درون اجزای ماژولار که می‌توانند به طور پویا در production تغییر حالت دهند کاهش می‌دهند. تکیه زیاد بر feature-flag-guarding یک الگوی رایج برای تحویل مداوم (Continuous Delivery) است که در فصل ۲۴ بیشتر بررسی می‌کنیم.

**بازخورد قابل دسترس و قابل عمل (Accessible and Actionable Feedback)**

همچنین مهم است که بازخورد از CI به طور گسترده قابل دسترس باشد. علاوه بر فرهنگ باز ما در مورد قابلیت دید کد، ما در مورد گزارش‌دهی تست خود نیز احساس مشابهی داریم. ما یک سیستم گزارش‌دهی تست یکپارچه داریم که در آن هر کسی به راحتی می‌تواند یک ساخت یا اجرای تست را جستجو کند، از جمله تمام لاگ‌ها (به استثنای اطلاعات شناسایی شخصی کاربر [PII])، چه برای اجرای محلی یک مهندس فردی و چه در یک ساخت خودکار development یا staging.

علاوه بر لاگ‌ها، سیستم گزارش‌دهی تست ما تاریخچه مفصلی از زمانی که اهداف ساخت یا تست شروع به شکست کردن ارائه می‌دهد، از جمله ممیزی‌هایی از اینکه ساخت در هر اجرا کجا بریده شد، کجا اجرا شد و توسط چه کسی. ما همچنین سیستمی برای طبقه‌بندی flake داریم که از آمار برای طبقه‌بندی flakeها در سطح کل گوگل استفاده می‌کند، بنابراین مهندسان نیازی ندارند خودشان این را بفهمند تا تعیین کنند آیا تغییر آن‌ها تست پروژه دیگری را شکسته (اگر تست flaky باشد: احتمالاً نه).

دید به تاریخچه تست به مهندسان قدرت می‌دهد تا بازخورد را به اشتراک بگذارند و با همکاری کنند، یک الزام حیاتی برای تیم‌های متفاوت برای تشخیص و یادگیری از شکست‌های یکپارچه‌سازی بین سیستم‌هایشان. به همین ترتیب، باگ‌ها (مثلاً تیکت‌ها یا issues) در گوگل با تاریخچه کامل نظرات برای همه باز هستند تا ببینند و یاد بگیرند (به استثنای PII مشتری).

در نهایت، هر بازخوردی از تست‌های CI نه تنها باید قابل دسترس بلکه قابل عمل باشد — آسان برای استفاده برای یافتن و رفع مشکلات.

![Section](images/page009-509-img1.png)

![Section](images/page010-510.png)

![Section](images/page011-511.png)

![Section](images/page012-512.png)

---

###### 📄 صفحه ۵۱۳
> 8 Each team at Google configures a subset of its project's tests to run on presubmit (versus post-submit). In
> reality, our continuous build actually optimizes some presubmit tests to be saved for post-submit, behind the
> scenes. We'll further discuss this later on in this chapter.
> and though generally rare, it happens most days at our scale. CI systems for smaller
> repositories or projects can avoid this problem by serializing submits so that there is
> no difference between what is about to enter and what just did.
> Presubmit versus post-submit
> So, which tests should be run on presubmit? Our general rule of thumb is: only fast,
> reliable ones. You can accept some loss of coverage on presubmit, but that means you
> need to catch any issues that slip by on post-submit, and accept some number of roll‐
> backs. On post-submit, you can accept longer times and some instability, as long as
> you have proper mechanisms to deal with it.
> We'll show how TAP and our case study handle failure manage‐
> ment in "CI at Google" on page 493.
> We don't want to waste valuable engineer productivity by waiting too long for slow
> tests or for too many tests—we typically limit presubmit tests to just those for the
> project where the change is happening. We also run tests concurrently, so there is a
> resource decision to consider as well. Finally, we don't want to run unreliable tests on
> presubmit, because the cost of having many engineers affected by them, debugging
> the same problem that is not related to their code change, is too high.
> Most teams at Google run their small tests (like unit tests) on presubmit8—these are
> the obvious ones to run as they tend to be the fastest and most reliable. Whether and
> how to run larger-scoped tests on presubmit is the more interesting question, and
> this varies by team. For teams that do want to run them, hermetic testing is a proven
> approach to reducing their inherent instability. Another option is to allow large-
> scoped tests to be unreliable on presubmit but disable them aggressively when they
> start failing.
> Release candidate testing
> After a code change has passed the CB (this might take multiple cycles if there were
> failures), it will soon encounter CD and be included in a pending release candidate.
> As CD builds RCs, it will run larger tests against the entire candidate. We test a
> release candidate by promoting it through a series of test environments and testing it
> at each deployment. This can include a combination of sandboxed, temporary envi‐
> 486
> |
> Chapter 23: Continuous Integration

**Presubmit در مقابل Post-submit و تست کردن Release Candidate**

پس، چه تست‌هایی باید روی presubmit اجرا شوند؟ قاعده کلی ما این است: فقط تست‌های سریع و قابل اعتماد. شما می‌توانید برخی از دست رفتن پوشش را روی presubmit بپذیرید، اما این به این معنی است که باید هر مشکلی که از غربال رد می‌شود را در post-submit شکار کنید و تعدادی بازگشت (rollback) را بپذیرید. در post-submit، می‌توانید زمان‌های طولانی‌تر و برخی ناپایداری‌ها را بپذیرید، تا زمانی که مکانیسم‌های مناسبی برای مقابله با آن داشته باشید.

ما نمی‌خواهیم بهره‌وری ارزشمند مهندسان را با صبر کردن زیاد برای تست‌های کند یا تعداد زیاد تست‌ها هدر دهیم — ما معمولاً تست‌های presubmit را فقط به تست‌های پروژه‌ای محدود می‌کنیم که تغییر در آن اتفاق می‌افتد. ما همچنین تست‌ها را به طور همزمان اجرا می‌کنیم، بنابراین تصمیم منابعی نیز برای در نظر گرفتن وجود دارد. در نهایت، ما نمی‌خواهیم تست‌های غیرقابل اعتماد را روی presubmit اجرا کنیم، زیرا هزینه تأثیر گذاشتن بر بسیاری از مهندسان توسط آن‌ها، دیباگ کردن مشکلی که به تغییر کد آن‌ها مربوط نیست، بسیار زیاد است.

بیشتر تیم‌ها در گوگل تست‌های کوچک خود (مانند تست‌های واحد) را روی presubmit اجرا می‌کنند — اینها واضح‌ترین تست‌ها برای اجرا هستند زیرا معمولاً سریع‌ترین و قابل اعتمادترین هستند. اینکه آیا و چگونه تست‌های با دامنه بزرگتر را روی presubmit اجرا کنیم سؤال جالب‌تری است و این بسته به تیم متفاوت است. برای تیم‌هایی که می‌خواهند آن‌ها را اجرا کنند، تست hermetic رویکردی اثبات شده برای کاهش ناپایداری ذاتی آن‌ها است. گزینه دیگر این است که اجازه دهیم تست‌های با دامنه بزرگ روی presubmit ناپایدار باشند اما وقتی شروع به شکست کردن می‌کنند آن‌ها را به شدت غیرفعال کنیم.

**تست کردن Release Candidate (Release Candidate Testing)**

پس از اینکه یک تغییر کد از CB عبور کرد (این ممکن است در صورت وجود شکست‌ها چندین چرخه طول بکشد)، به زودی با CD مواجه شده و در یک release candidate در انتظار گنجانده می‌شود. با ساخت RCها توسط CD، تست‌های بزرگتری روی کل کاندیدا اجرا خواهد شد. ما یک release candidate را با ارتقای آن از طریق سریعی از محیط‌های تست و تست کردن آن در هر استقرار آزمایش می‌کنیم.

![Section](images/page013-513-img1.png)

![Section](images/page014-514-img1.png)

![Section](images/page015-515.png)

![Section](images/page016-516.png)

---

###### 📄 صفحه ۵۱۷
> CI Challenges
> We've discussed some of the established best practices in CI and have introduced
> some of the challenges involved, such as the potential disruption to engineer produc‐
> tivity of unstable, slow, conflicting, or simply too many tests at presubmit. Some com‐
> mon additional challenges when implementing CI include the following:
> • Presubmit optimization, including which tests to run at presubmit time given the
> potential issues we've already described, and how to run them.
> • Culprit finding and failure isolation: Which code or other change caused the
> problem, and which system did it happen in? "Integrating upstream microservi‐
> ces" is one approach to failure isolation in a distributed architecture, when you
> want to figure out whether a problem originated in your own servers or a back‐
> end. In this approach, you stage combinations of your stable servers along with
> upstream microservices' new servers. (Thus, you are integrating the microservi‐
> ces' latest changes into your testing.) This approach can be particularly challeng‐
> ing due to version skew: not only are these environments often incompatible, but
> you're also likely to encounter false positives—problems that occur in a particular
> staged combination that wouldn't actually be spotted in production.
> • Resource constraints: Tests need resources to run, and large tests can be very
> expensive. In addition, the cost for the infrastructure for inserting automated
> testing throughout the process can be considerable.
> There's also the challenge of failure management—what to do when tests fail.
> Although smaller problems can usually be fixed quickly, many of our teams find that
> it's extremely difficult to have a consistently green test suite when large end-to-end
> tests are involved. They inherently become broken or flaky and are difficult to debug;
> there needs to be a mechanism to temporarily disable and keep track of them so that
> the release can go on. A common technique at Google is to use bug "hotlists" filed by
> an on-call or release engineer and triaged to the appropriate team. Even better is
> when these bugs can be automatically generated and filed—some of our larger prod‐
> ucts, like Google Web Server (GWS) and Google Assistant, do this. These hotlists
> should be curated to make sure any release-blocking bugs are fixed immediately.
> Nonrelease blockers should be fixed, too; they are less urgent, but should also be pri‐
> oritized so the test suite remains useful and is not simply a growing pile of disabled,
> old tests. Often, the problems caught by end-to-end test failures are actually with tests
> rather than code.
> Flaky tests pose another problem to this process. They erode confidence similar to a
> broken test, but finding a change to roll back is often more difficult because the fail‐
> ure won't happen all the time. Some teams rely on a tool to remove such flaky tests
> from presubmit temporarily while the flakiness is investigated and fixed. This keeps
> confidence high while allowing for more time to fix the problem.
> 490
> |
> Chapter 23: Continuous Integration

**چالش‌های CI**

ما برخی از بهترین شیوه‌های-established CI را بحث کرده‌ایم و برخی از چالش‌های مرتبط را معرفی کرده‌ایم، مانند اختلال بالقوه در بهره‌وری مهندسان ناشی از تست‌های ناپایدار، کند، متعارض یا به سادگی بیش از حد زیاد در presubmit. برخی چالش‌های اضافی رایج هنگام پیاده‌سازی CI شامل موارد زیر هستند:

• بهینه‌سازی presubmit، از جمله اینکه کدام تست‌ها را در زمان presubmit با توجه به مشکلات بالقوه‌ای که قبلاً توصیف کرده‌ایم اجرا کنیم و چگونه آن‌ها را اجرا کنیم.
• یافتن مقصر و ایزوله کردن شکست: کدام کد یا تغییر دیگر مشکل را ایجاد کرد و در کدام سیستم رخ داد؟ «ادغام microservices upstream» یک رویکرد برای ایزوله کردن شکست در معماری توزیع‌شده است، زمانی که می‌خواهید بفهمید آیا مشکل از سرورهای خودتان یا backend نشأت گرفته. در این رویکرد، ترکیباتی از سرورهای پایدار خود را با سرورهای جدید microservices upstream آماده‌سازی (stage) می‌کنید. این رویکرد می‌تواند به دلیل version skew به ویژه چالش‌برانگیز باشد: نه تنها این محیط‌ها اغلب ناسازگار هستند، بلکه احتمالاً با مثبت‌های کاذب مواجه خواهید شد — مشکلاتی که در یک ترکیب آماده‌سازی خاص رخ می‌دهند اما در production واقعاً شناسایی نمی‌شوند.
• محدودیت‌های منابع: تست‌ها برای اجرا به منابع نیاز دارند و تست‌های بزرگ می‌توانند بسیار پرهزینه باشند. علاوه بر این، هزینه زیرساخت برای درج تست خودکار در سراسر فرآیند می‌تواند قابل توجه باشد.

چالش مدیریت شکست — وقتی تست‌ها شکست می‌خورند چه کاری انجام دهیم — نیز وجود دارد. اگرچه مشکلات کوچکتر معمولاً می‌توانند به سرعت حل شوند، بسیاری از تیم‌های ما دریافته‌اند که داشتن یک مجموعه تست سبز (موفق) به طور مداوم زمانی که تست‌های بزرگ end-to-end درگیر هستند بسیار دشوار است. آن‌ها ذاتاً شکسته یا flaky می‌شوند و دیباگ کردن آن‌ها دشوار است؛ باید مکانیسمی برای غیرفعال کردن موقت و ردیابی آن‌ها وجود داشته باشد تا انتشار بتواند ادامه یابد. یک تکنیک رایج در گوگل استفاده از «hotlist» باگ‌ها است که توسط مهندس on-call یا release ثبت شده و به تیم مناسب ارجاع داده می‌شود. بهتر از آن زمانی است که این باگ‌ها بتوانند به طور خودکار تولید و ثبت شوند — برخی از محصولات بزرگتر ما مانند Google Web Server (GWS) و Google Assistant این کار را انجام می‌دهند.

تست‌های flaky مشکل دیگری برای این فرآیند ایجاد می‌کنند. آن‌ها اطمینان را مانند یک تست شکسته فرسایش می‌دهند، اما یافتن تغییری برای بازگرداندن اغلب دشوارتر است زیرا شکست همیشه رخ نمی‌دهد. برخی تیم‌ها به ابزاری تکیه می‌کنند تا این تست‌های flaky را به طور موقت از presubmit حذف کند در حالی که flakiness بررسی و رفع می‌شود. این اطمینان را بالا نگه می‌دارد در حالی که زمان بیشتری برای رفع مشکل فراهم می‌کند.

![Section](images/page017-517.png)

![Section](images/page018-518.png)

![Section](images/page019-519.png)

![Section](images/page020-520.png)

![Section](images/page021-521.png)

![Section](images/page022-522.png)

![Section](images/page023-523.png)

![Section](images/page024-524.png)

---