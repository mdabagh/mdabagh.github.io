> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۴۸۱
> 19 Often through trial and error.
> Above and beyond the nebulous "We look bad," there are also parts of this story that
> illustrate how we can be subject to technical problems stemming from poorly
> released/poorly maintained external dependencies. Although the flags library was
> shared but ignored, there were still some Google-backed open source projects, or
> projects that needed to be shareable outside of our monorepo ecosystem. Unsurpris‐
> ingly, the authors of those other projects were able to identify19 the common API sub‐
> set between the internal and external forks of that library. Because that common
> subset stayed fairly stable between the two versions for a long period, it silently
> became "the way to do this" for the rare teams that had unusual portability require‐
> ments between roughly 2008 and 2017. Their code could build in both internal and
> external ecosystems, switching out forked versions of the flags library depending on
> environment.
> Then, for unrelated reasons, C++ library teams began tweaking observable-but-not-
> documented pieces of the internal flag implementation. At that point, everyone who
> was depending on the stability and equivalence of an unsupported external fork
> started screaming that their builds and releases were suddenly broken. An optimiza‐
> tion opportunity worth some thousands of aggregate CPUs across Google's fleet was
> significantly delayed, not because it was difficult to update the API that 250 million
> lines of code depended upon, but because a tiny handful of projects were relying on
> unpromised and unexpected things. Once again, Hyrum's Law affects software
> changes, in this case even for forked APIs maintained by separate organizations.
> Case Study: AppEngine
> A more serious example of exposing ourselves to greater risk of unexpected technical
> dependency comes from publishing Google's AppEngine service. This service allows
> users to write their applications on top of an existing framework in one of several
> popular programming languages. So long as the application is written with a proper
> storage/state management model, the AppEngine service allows those applications to
> scale up to huge usage levels: backing storage and frontend management are managed
> and cloned on demand by Google's production infrastructure.
> Originally, AppEngine's support for Python was a 32-bit build running with an older
> version of the Python interpreter. The AppEngine system itself was (of course) imple‐
> mented in our monorepo and built with the rest of our common tools, in Python and
> in C++ for backend support. In 2014 we started the process of doing a major update
> to the Python runtime alongside our C++ compiler and standard library installations,
> with the result being that we effectively tied "code that builds with the current C++
> compiler" to "code that uses the updated Python version"—a project that upgraded
> one of those dependencies inherently upgraded the other at the same time. For most
> 454
> |
> Chapter 21: Dependency Management

**وابستگی‌های خارجی و مطالعه موردی AppEngine**

فراتر از «ما بد به نظر می‌رسیم» مبهم، بخش‌هایی از این داستان نیز وجود دارد که نشان می‌دهد چگونه می‌توانیم در معرض مشکلات فنی ناشی از وابستگی‌های خارجی ضعیف منتشر شده/ضعیف نگهداری شده قرار بگیریم. اگرچه کتابخانه flags مشترک اما نادیده گرفته شده بود، هنوز پروژه‌های متن‌بازی با حمایت گوگل، یا پروژه‌هایی که نیاز به اشتراک‌گذاری خارج از اکوسیستم monorepo ما داشتند وجود داشت. تعجب‌آور نیست که نویسندگان آن پروژه‌های دیگر توانستند زیرمجموعه API مشترک بین forkهای داخلی و خارجی آن کتابخانه را شناسایی کنند. از آنجا که آن زیرمجموعه مشترک برای مدت طولانی بین دو نسخه نسبتاً پایدار باقی ماند، به آرامی به «راه انجام این کار» برای تیم‌های نادری تبدیل شد که الزامات قابلیت حمل غیرمعمولی بین حدود ۲۰۰۸ تا ۲۰۱۷ داشتند. کد آن‌ها می‌توانست در هر دو اکوسیستم داخلی و خارجی ساخته شود و نسخه‌های fork شده کتابخانه flags را بسته به محیط عوض کند.

سپس، به دلایل غیرمرتبط، تیم‌های کتابخانه C++ شروع به تغییر بخش‌های قابل مشاهده اما مستند نشده پیاده‌سازی پرچم داخلی کردند. در آن نقطه، هر کسی که به پایداری و معادل بودن یک fork خارجی پشتیبانی نشده وابسته بود شروع به فریاد زدن کرد که ساختها و انتشارات آن‌ها ناگهان شکسته شده است. فرصت بهینه‌سازی ارزش چند هزار CPU تجمیعی در ناوگان گوگل به طور قابل توجهی به تأخیر افتاد، نه به این دلیل که به‌روزرسانی API که ۲۵۰ میلیون خط کد به آن وابسته بود دشوار بود، بلکه به این دلیل که تعداد کمی از پروژه‌ها به چیزهایی غیرمنتظره و بدون وعده وابسته بودند. یک بار دیگر، قانون Hyrum بر تغییرات نرم‌افزار تأثیر می‌گذارد، در این مورد حتی برای APIهای fork شده که توسط سازمان‌های جداگانه نگهداری می‌شوند.

**مطالعه موردی: AppEngine (Case Study: AppEngine)**

مثال جدی‌تری از قرار گرفتن در معرض خطر بیشتر وابستگی فنی غیرمنتظره از انتشار سرویس AppEngine گوگل می‌آید. این سرویس به کاربران اجازه می‌دهد برنامه‌های خود را روی یک فریم‌ورک موجود به یکی از چندین زبان برنامه‌نویسی محبوب بنویسند. تا زمانی که برنامه با مدل ذخیره‌سازی/مدیریت state مناسب نوشته شده باشد، سرویس AppEngine به آن برنامه‌ها اجازه می‌دهد تا سطوح استفاده عظیمی مقیاس‌پذیر شوند: ذخیره‌سازی پشتیبانی و مدیریت رابط کاربری توسط زیرساخت تولیدی گوگل به صورت تقاضایی مدیریت و کلون می‌شوند.

در ابتدا، پشتیبانی AppEngine از جاوا یک ساخت ۳۲ بیتی بود که با نسخه قدیمی‌تر مفسر جاوا اجرا می‌شد. خود سیستم AppEngine (البته) در monorepo ما پیاده‌سازی شده بود و با بقیه ابزارهای مشترک ما در جاوا و C++ برای پشتیبانی backend ساخته می‌شد. در سال ۲۰۱۴ فرآیند انجام به‌روزرسانی اصلی زمان اجرای جاوا را در کنار نصب‌های کامپایلر C++ و کتابخانه استاندارد خود آغاز کردیم، و نتیجه این بود که ما عمداً «کدی که با کامپایلر C++ فعلی ساخته می‌شود» را به «کدی که از نسخه به‌روز شده جاوا استفاده می‌کند» متصل کردیم — پروژه‌ای که یکی از آن وابستگی‌ها را ارتقا می‌داد ذاتاً دیگری را همزمان ارتقا می‌داد.

![Section](images/page001-481.png)

![Section](images/page002-482.png)

![Section](images/page003-483.png)

![Section](images/page004-484.png)

---

###### 📄 صفحه ۴۸۵


![Section](images/page005-485.png)

![Section](images/page006-486.png)

![Section](images/page007-487.png)

![Section](images/page008-488.png)

---

###### 📄 صفحه ۴۸۹
> the costs of migration will be borne somewhere in the organization. Centralizing the
> migration and accounting for its costs is almost always faster and cheaper than
> depending on individual teams to organically migrate.
> Additionally, having teams that own the systems requiring LSCs helps align incen‐
> tives to ensure the change gets done. In our experience, organic migrations are
> unlikely to fully succeed, in part because engineers tend to use existing code as exam‐
> ples when writing new code. Having a team that has a vested interest in removing the
> old system responsible for the migration effort helps ensure that it actually gets done.
> Although funding and staffing a team to run these kinds of migrations can seem like
> an additional cost, it is actually just internalizing the externalities that an unfunded
> mandate creates, with the additional benefits of economies of scale.
> Case Study: Filling Potholes
> Although the LSC systems at Google are used for high-priority migrations, we've also
> discovered that just having them available opens up opportunities for various small
> fixes across our codebase, which just wouldn't have been possible without them.
> Much like transportation infrastructure tasks consist of building new roads as well as
> repairing old ones, infrastructure groups at Google spend a lot of time fixing existing
> code, in addition to developing new systems and moving users to them.
> For example, early in our history, a template library emerged to supplement the C++
> Standard Template Library. Aptly named the Google Template Library, this library
> consisted of several header files' worth of implementation. For reasons lost in the
> mists of time, one of these header files was named stl_util.h and another was named
> map-util.h (note the different separators in the file names). In addition to driving the
> consistency purists nuts, this difference also led to reduced productivity, and engi‐
> neers had to remember which file used which separator, and only discovered when
> they got it wrong after a potentially lengthy compile cycle.
> Although fixing this single-character change might seem pointless, particularly across
> a codebase the size of Google's, the maturity of our LSC tooling and process enabled
> us to do it with just a couple weeks' worth of background-task effort. Library authors
> could find and apply this change en masse without having to bother end users of
> these files, and we were able to quantitatively reduce the number of build failures
> caused by this specific issue. The resulting increases in productivity (and happiness)
> more than paid for the time to make the change.
> As the ability to make changes across our entire codebase has improved, the diversity
> of changes has also expanded, and we can make some engineering decisions knowing
> that they aren't immutable in the future. Sometimes, it's worth the effort to fill a few
> potholes.
> 462
> |
> Chapter 22: Large-Scale Changes

**هزینه‌های مهاجرت و مطالعه موردی پر کردن چاله‌ها**

هزینه‌های مهاجرت در جایی در سازمان تحمل خواهد شد. متمرکز کردن مهاجرت و در نظر گرفتن هزینه‌های آن تقریباً همیشه سریع‌تر و ارزان‌تر از وابسته بودن به تیم‌های فردی برای مهاجرت ارگانیک است.

علاوه بر این، داشتن تیم‌هایی که سیستم‌های نیازمند LSC را مالکیت می‌کنند به هم‌راستایی انگیزه‌ها برای تضمین انجام تغییر کمک می‌کند. در تجربه ما، مهاجرت‌های ارگانیک احتمالاً به طور کامل موفق نمی‌شوند، تا حدی به این دلیل که مهندسان تمایل دارند از کد موجود به عنوان الگو هنگام نوشتن کد جدید استفاده کنند. داشتن تیمی که منافعی در حذف سیستم قدیمی دارد و مسئول تلاش مهاجرت است به تضمین انجام واقعی آن کمک می‌کند. اگرچه تأمین بودجه و کارکنان تیمی برای اجرای این نوع مهاجرت‌ها می‌تواند هزینه اضافی به نظر برسد، در واقع فقط داخلی کردن externalitiesهایی است که یک دستور بدون بودجه ایجاد می‌کند، با مزایای اضافی صرفه‌جویی ناشی از مقیاس.

**مطالعه موردی: پر کردن چاله‌ها (Case Study: Filling Potholes)**

اگرچه سیستم‌های LSC در گوگل برای مهاجرت‌های با اولویت بالا استفاده می‌شوند، ما همچنین کشف کرده‌ایم که فقط در دسترس بودن آن‌ها فرصت‌هایی برای تعمیرات کوچک مختلف در سراسر پایگاه کد ما باز می‌کند که بدون آن‌ها امکان‌پذیر نبود. درست مانند وظایف زیرساخت حمل و نقل که شامل ساخت جاده‌های جدید و همچنین تعمیر جاده‌های قدیمی می‌شود، گروه‌های زیرساخت در گوگل زمان زیادی صرف تعمیر کد موجود می‌کنند، علاوه بر توسعه سیستم‌های جدید و انتقال کاربران به آن‌ها.

برای مثال، در اوایل تاریخ ما، یک کتابخانه template برای تکمیل کتابخانه Standard Template Library جاوا ظاهر شد. این کتابخانه که به درستی Google Template Library نامیده شد، از چندین فایل header پیاده‌سازی تشکیل شده بود. به دلایلی که در ابهام زمان گم شده‌اند، یکی از این فایل‌های header stl_util.h و دیگری map-util.h نام داشت (جدایگرهای متفاوت در نام فایل‌ها را توجه کنید). علاوه بر دیوانه کردن طرفداران سازگاری، این تفاوت همچنین منجر به کاهش بهره‌وری شد و مهندسان باید به یاد می‌آوردند کدام فایل از کدام جداگنده استفاده می‌کند، و فقط زمانی متوجه اشتباه خود می‌شدند که پس از چرخه کامپایل بالقوه طولانی آن را کشف می‌کردند.

اگرچه رفع این تغییر تک کاراکتری ممکن است بی‌فایده به نظر برسد، به ویژه در پایگاه کدی به اندازه پایگاه کد گوگل، بلوغ ابزارها و فرآیند LSC ما به ما اجازه داد آن را تنها با چند هفته تلاش وظیفه پس‌زمینه انجام دهیم. نویسندگان کتابخانه می‌توانستند این تغییر را به صورت گسترده پیدا و اعمال کنند بدون اینکه کاربران نهایی این فایل‌ها را آزار دهند، و ما توانستیم به طور کمّی تعداد شکست‌های ساخت ناشی از این مشکل خاص را کاهش دهیم. افزایش حاصل در بهره‌وری (و شادی) بیش از زمان صرف شده برای انجام تغییر ارزش داشت.

با بهبود قابلیت ایجاد تغییرات در سراسر پایگاه کد ما، تنوع تغییرات نیز گسترش یافته و می‌توانیم برخی تصمیمات مهندسی را با دانستن اینکه در آینده تغییرناپذیر نیستند بگیریم. گاهی اوقت، ارزش تلاش کردن برای پر کردن چند چاله را دارد.

![Section](images/page009-489.png)

![Section](images/page010-490.png)

![Section](images/page011-491.png)

![Section](images/page012-492.png)

---

###### 📄 صفحه ۴۹۳
> 7 The largest series of LSCs ever executed removed more than one billion lines of code from the repository over
> the course of three days. This was largely to remove an obsolete part of the repository that had been migrated
> to a new home; but still, how confident do you have to be to delete one billion lines of code?
> 8 LSCs are usually supported by tools that make finding, making, and reviewing changes relatively straight
> forward.
> Case Study: Testing LSCs
> Adam Bender
> Today it is common for a double-digit percentage (10% to 20%) of the changes in a
> project to be the result of LSCs, meaning a substantial amount of code is changed in
> projects by people whose full-time job is unrelated to those projects. Without good
> tests, such work would be impossible, and Google's codebase would quickly atrophy
> under its own weight. LSCs enable us to systematically migrate our entire codebase to
> newer APIs, deprecate older APIs, change language versions, and remove popular but
> dangerous practices.
> Even a simple one-line signature change becomes complicated when made in a thou‐
> sand different places across hundreds of different products and services.7 After the
> change is written, you need to coordinate code reviews across dozens of teams. Lastly,
> after reviews are approved, you need to run as many tests as you can to be sure the
> change is safe.8 We say "as many as you can," because a good-sized LSC could trigger a
> rerun of every single test at Google, and that can take a while. In fact, many LSCs have
> to plan time to catch downstream clients whose code backslides while the LSC makes
> its way through the process.
> Testing an LSC can be a slow and frustrating process. When a change is sufficiently
> large, your local environment is almost guaranteed to be permanently out of sync
> with head as the codebase shifts like sand around your work. In such circumstances,
> it is easy to find yourself running and rerunning tests just to ensure your changes
> continue to be valid. When a project has flaky tests or is missing unit test coverage, it
> can require a lot of manual intervention and slow down the entire process. To help
> speed things up, we use a strategy called the TAP (Test Automation Platform) train.
> Riding the TAP Train
> The core insight to LSCs is that they rarely interact with one another, and most affec‐
> ted tests are going to pass for most LSCs. As a result, we can test more than one
> change at a time and reduce the total number of tests executed. The train model has
> proven to be very effective for testing LSCs.
> The TAP train takes advantage of two facts:
> • LSCs tend to be pure refactorings and therefore very narrow in scope, preserving
> local semantics.
> 466
> |
> Chapter 22: Large-Scale Changes

**مطالعه موردی: تست کردن LSC و TAP Train**

امروزه رایج است که درصد دو رقمی (۱۰٪ تا ۲۰٪) تغییرات در یک پروژه نتیجه LSC باشد، به این معنی که مقدار قابل توجهی کد در پروژه‌ها توسط افرادی تغییر می‌کند که شغل تمام‌وقت آن‌ها به آن پروژه‌ها مربوط نیست. بدون تست‌های خوب، چنین کاری غیرممکن بود و پایگاه کد گوگل به سرعت تحت وزن خود تحلیل می‌رفت. LSCها به ما امکان می‌دهند تمام پایگاه کد خود را به طور سیستماتیک به APIهای جدیدتر مهاجرت دهیم، APIهای قدیمی را منسوخ کنیم، نسخه‌های زبان را تغییر دهیم و شیوه‌های محبوب اما خطرناک را حذف کنیم.

حتی یک تغییر ساده امضای یک خطی وقتی در هزاران مکان مختلف در صدها محصول و سرویس مختلف انجام شود پیچیده می‌شود. پس از نوشتن تغییر، باید بررسی‌های کد را در ده‌ها تیم هماهنگ کنید. در نهایت، پس از تأیید بررسی‌ها، باید تعداد تست‌هایی که می‌توانید را اجرا کنید تا مطمئن شوید تغییر ایمن است. ما «تعدادی که می‌توانید» می‌گوییم زیرا یک LSC با اندازه مناسب می‌تواند اجرای مجدد هر تست واحد در گوگل را فعال کند و این ممکن است مدتی طول بکشد.

تست کردن یک LSC می‌تواند فرآیندی کند و ناامیدکننده باشد. وقتی تغییر به اندازه کافی بزرگ است، محیط محلی شما تقریباً به طور دائم از همگام بودن با head خارج می‌شود زیرا پایگاه کد مانند شن اطراف کار شما جابجا می‌شود. در چنین شرایطی، به راحتی می‌توان خود را در حال اجرا و اجرای مجدد تست‌ها یافت فقط برای اطمینان از اینکه تغییرات شما همچنان معتبر هستند. وقتی پروژه تست‌های ناپایدار (flaky) دارد یا پوشش تست واحد ندارد، می‌تواند به مداخله دستی زیادی نیاز داشته باشد و کل فرآیند را کند کند. برای کمک به تسریع امور، ما از استراتژی به نام TAP (پلتفرم تست خودکار) train استفاده می‌کنیم.

**سوار شدن TAP Train (Riding the TAP Train)**

بینش اصلی LSCها این است که آن‌ها به ندرت با یکدیگر تعامل دارند و بیشتر تست‌های تحت تأثیر برای بیشتر LSCها رد خواهند شد. در نتیجه، می‌توانیم بیش از یک تغییر را در یک زمان تست کنیم و تعداد کل تست‌های اجرا شده را کاهش دهیم. مدل train ثابت کرده است که برای تست کردن LSCها بسیار مؤثر است.

TAP train از دو واقعیت بهره می‌برد:
• LSCها تمایل به refactorings خالص دارند و بنابراین از نظر دامنه بسیار باریک هستند و معنای محلی را حفظ می‌کنند.

![Section](images/page013-493-img1.png)

![Section](images/page014-494.png)

![Section](images/page015-495.png)

![Section](images/page016-496.png)

---

###### 📄 صفحه ۴۹۷
> a solid historic track record of improvements have generated widespread endorse‐
> ment of LSCs throughout Google.
> Codebase Insight
> To do LSCs, we've found it invaluable to be able to do large-scale analysis of our code‐
> base, both on a textual level using traditional tools, as well as on a semantic level. For
> example, Google's use of the semantic indexing tool Kythe provides a complete map
> of the links between parts of our codebase, allowing us to ask questions such as
> "Where are the callers of this function?" or "Which classes derive from this one?"
> Kythe and similar tools also provide programmatic access to their data so that they
> can be incorporated into refactoring tools. (For further examples, see Chapters 17 and
> 20.)
> We also use compiler-based indices to run abstract syntax tree-based analysis and
> transformations over our codebase. Tools such as ClangMR, JavacFlume, or Refaster,
> which can perform transformations in a highly parallelizable way, depend on these
> insights as part of their function. For smaller changes, authors can use specialized,
> custom tools, perl or sed, regular expression matching, or even a simple shell script.
> Whatever tool your organization uses for change creation, it's important that its
> human effort scale sublinearly with the codebase; in other words, it should take
> roughly the same amount of human time to generate the collection of all required
> changes, no matter the size of the repository. The change creation tooling should also
> be comprehensive across the codebase, so that an author can be assured that their
> change covers all of the cases they're trying to fix.
> As with other areas in this book, an early investment in tooling usually pays off in the
> short to medium term. As a rule of thumb, we've long held that if a change requires
> more than 500 edits, it's usually more efficient for an engineer to learn and execute
> our change-generation tools rather than manually execute that edit. For experienced
> "code janitors," that number is often much smaller.
> Change Management
> Arguably the most important piece of large-scale change infrastructure is the set of
> tooling that shards a master change into smaller pieces and manages the process of
> testing, mailing, reviewing, and committing them independently. At Google, this tool
> is called Rosie, and we discuss its use more completely in a few moments when we
> examine our LSC process. In many respects, Rosie is not just a tool, but an entire
> platform for making LSCs at Google scale. It provides the ability to split the large sets
> of comprehensive changes produced by tooling into smaller shards, which can be tes‐
> ted, reviewed, and submitted independently.
> 470
> |
> Chapter 22: Large-Scale Changes

**بینش پایگاه کد و مدیریت تغییرات**

برای انجام LSCها، ما فهمیده‌ایم که توانایی انجام تحلیل مقیاس بزرگ از پایگاه کد ما، هم در سطح متنی با استفاده از ابزارهای سنتی و هم در سطح معنایی، ارزشمند است. برای مثال، استفاده گوگل از ابزار فهرست‌گذاری معنایی Kythe نقشه کاملی از پیوندهای بین بخش‌های پایگاه کد ما فراهم می‌کند و به ما امکان می‌دهد سؤالاتی مانند «فراخوان‌های این تابع کجا هستند؟» یا «کدام کلاس‌ها از این کلاس مشتق شده‌اند؟» بپرسیم. Kythe و ابزارهای مشابه همچنین دسترسی برنامه‌نویسی به داده‌های خود فراهم می‌کنند تا بتوانند در ابزارهای بازآرایی (refactoring) ادغام شوند.

ما همچنین از ایندکس‌های مبتنی بر کامپایلر برای اجرای تحلیل و تبدیل‌های مبتنی بر درخت نحو انتزاعی (abstract syntax tree) روی پایگاه کد خود استفاده می‌کنیم. ابزارهایی مانند ClangMR، JavacFlume یا Refaster که می‌توانند تبدیل‌ها را به شیوه‌ای کاملاً موازی‌پذیر انجام دهند، به این بینش‌ها به عنوان بخشی از عملکرد خود وابسته هستند. برای تغییرات کوچکتر، نویسندگان می‌توانند از ابزارهای تخصصی سفارشی، perl یا sed، تطابق عبارت با قاعده (regular expression matching) یا حتی یک اسکریپت ساده shell استفاده کنند.

هر ابزاری که سازمان شما برای ایجاد تغییر استفاده می‌کند، مهم است که تلاش انسانی آن به صورت خطی کمتر از پایگاه کد مقیاس‌پذیر باشد؛ به عبارت دیگر، باید تقریباً مقدار یکسانی زمان انسانی برای تولید مجموعه تمام تغییرات مورد نیاز صرف شود، مهم نیت اندازه مخزن چقدر باشد. ابزارهای ایجاد تغییر همچنین باید در سراسر پایگاه کد جامع باشند، تا نویسنده مطمئن شود تغییرش تمام مواردی را که سعی در رفع آن‌ها دارد پوشش می‌دهد.

**مدیریت تغییرات (Change Management)**

به احتمال زیاد مهم‌ترین بخش زیرساخت تغییرات مقیاس بزرگ مجموعه ابزاری است که یک تغییر اصلی را به بخش‌های کوچکتر خرد می‌کند و فرآیند تست کردن، ایمیل زدن، بررسی کردن و commit کردن آن‌ها را به طور مستقل مدیریت می‌کند. در گوگل، این ابزار Rosie نام دارد و استفاده از آن را در چند لحظه هنگام بررسی فرآیند LSC خود به طور کامل‌تر بحث می‌کنیم. از بسیاری جهات، Rosie فقط یک ابزار نیست، بلکه یک پلتفرم کامل برای ایجاد LSC در مقیاس گوگل است. قابلیت تقسیم مجموعه‌های بزرگ تغییرات جامع تولید شده توسط ابزارها به قطعه‌های کوچکتر را فراهم می‌کند که می‌توانند به طور مستقل تست، بررسی و ارسال شوند.

![Section](images/page017-497.png)

![Section](images/page018-498.png)

![Section](images/page019-499.png)

![Section](images/page020-500.png)

---