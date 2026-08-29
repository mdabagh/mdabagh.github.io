> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۳۶۹
> 11 For instance, if there are external/third-party libraries that are periodically updated, it might be infeasible to
> update that library and update all use of it in a single atomic change. As such, it is often necessary to add a
> new version of that library, prevent new users from adding dependencies on the old one, and incrementally
> switch usage from old to new.
> In some cases, we might be able to hack things together in a way to allow a resulting
> executable to function correctly. Java, for instance, has a relatively standard practice
> called shading, which tweaks the names of the internal dependencies of a library to
> hide those dependencies from the rest of the application. When dealing with func‐
> tions, this is technically sound, even if it is theoretically a bit of a hack. When dealing
> with types that can be passed from one package to another, shading solutions work
> neither in theory nor in practice. As far as we know, any technological trickery that
> allows multiple isolated versions of a library to function in the same binary share this
> limitation: that approach will work for functions, but there is no good (efficient) solu‐
> tion to shading types—multiple versions for any library that provides a vocabulary
> type (or any higher-level construct) will fail. Shading and related approaches are
> patching over the underlying issue: multiple versions of the same dependency are
> needed. (We'll discuss how to minimize that in general in Chapter 21.)
> Any policy system that allows for multiple versions in the same codebase is allowing
> for the possibility of these costly incompatibilities. It's possible that you'll get away
> with it for a while (we certainly have a number of small violations of this policy), but
> in general, any multiple-version situation has a very real possibility of leading to big
> problems.
> The "One-Version" Rule
> With that example in mind, on top of the Single Source of Truth model, we can hope‐
> fully understand the depth of this seemingly simple rule for source control and
> branch management:
> Developers must never have a choice of "What version of this component should I
> depend upon?"
> Colloquially, this becomes something like a "One-Version Rule." In practice, "One-
> Version" is not hard and fast,11 but phrasing this around limiting the versions that can
> be chosen when adding a new dependency conveys a very powerful understanding.
> For an individual developer, lack of choice can seem like an arbitrary impediment.
> Yet we see again and again that for an organization, it's a critical component in effi‐
> cient scaling. Consistency has a profound importance at all levels in an organization.
> From one perspective, this is a direct side effect of discussions about consistency and
> ensuring the ability to leverage consistent "choke points."
> 342
> |
> Chapter 16: Version Control and Branch Management

**قانون "یک نسخه" (One-Version Rule)**

با در نظر گرفتن آن مثال، در کنار مدل Single Source of Truth، امیدواریم بتوانیم عمق این قانون به ظاهر ساده را برای کنترل منبع و مدیریت شاخه درک کنیم:

> توسعه‌دهندگان نباید هیچ‌وقت انتخابی داشته باشند که "کدام نسخه از این مؤلفه باید به آن وابسته باشم؟"

به بیان عامیانه، این تبدیل به چیزی شبیه "One-Version Rule" می‌شود. در عمل، "One-Version" قطعی و غیرقابل تغییر نیست، اما بیان آن حول محدود کردن نسخه‌هایی که هنگام اضافه کردن یک وابستگی جدید می‌توان انتخاب کرد، درک بسیار قدرتمندی منتقل می‌کند.

برای یک توسعه‌دهنده منفرد، نبود انتخاب ممکن است مانند یک مانع دلخواه به نظر برسد. اما بارها و بارها می‌بینیم که برای یک سازمان، این یک مؤلفه حیاتی در مقیاس‌دهی کارآمد است. Consistency (سازگاری) در تمام سطوح سازمان اهمیت عمیقی دارد. از یک دیدگاه، این عارضه مستقیم بحث‌های درباره consistency و تضمین توانایی بهره‌برداری از "choke points" (نقاط کنترل) سازگار است.

**چرا One-Version Rule مهم است؟**

وقتی چندین نسخه از یک مؤلفه در codebase وجود دارد، مشکلات زیادی ایجاد می‌شود:
- **ناسازگاری نسخه‌ها**: نسخه‌های مختلف ممکن است API متفاوتی داشته باشند
- **تداخل وابستگی‌ها**: مؤلفه‌های مختلف ممکن است نسخه‌های متفاوتی از یک کتابخانه را نیاز داشته باشند
- **پیچیدگی build**: سیستم build باید بتواند با چندین نسخه کار کند
- **مشکلات runtime**: ناسازگاری‌ها ممکن است در حین اجرا ظاهر شوند

یکی از رایج‌ترین نقض‌های این قانون، استفاده از نسخه‌های مختلف یک کتابخانه در بخش‌های مختلف codebase است. این ممکن است در کوتاه‌مدت کار کند، اما در درازمدت منجر به مشکلات جدی می‌شود.


![Section](images/page001-369.png)

![Section](images/page002-370.png)

![Section](images/page003-371.png)

![Section](images/page004-372.png)

---

###### 📄 صفحه ۳۷۳
> 16 We don't think we've seen anything do this particularly smoothly, but the interrepository dependencies/virtual
> monorepo idea is clearly in the air.
> 17 Or you have the willingness and capability to customize your VCS—and maintain that customization for the
> lifetime of your codebase/organization. Then again, maybe don't plan on that as an option; that is a lot of
> overhead.
> Software engineering tools including both VCS and build systems are increasingly
> providing mechanisms to smartly blend between fine-grained repositories and mon‐
> orepos to provide an experience akin to the monorepo—an agreed-upon ordering of
> commits and understanding of the dependency graph. Git submodules, Bazel with
> external dependencies, and CMake subprojects all allow modern developers to syn‐
> thesize something weakly approximating monorepo behavior without the costs and
> downsides of a monorepo.16 For instance, fine-grained repositories are easier to deal
> with in terms of scale (Git often has performance issues after a few million commits
> and tends to be slow to clone when repositories include large binary artifacts) and
> storage (VCS metadata can add up, especially if you have binary artifacts in your ver‐
> sion control system). Fine-grained repositories in a federated/virtual-monorepo
> (VMR)–style repository can make it easier to isolate experimental or top-secret
> projects while still holding to One Version and allowing access to common utilities.
> To put it another way: if every project in your organization has the same secrecy,
> legal, privacy, and security requirements,17 a true monorepo is a fine way to go.
> Otherwise, aim for the functionality of a monorepo, but allow yourself the flexibility
> of implementing that experience in a different fashion. If you can manage with dis‐
> joint repositories and adhere to One Version or your workload is all disconnected
> enough to allow truly separate repositories, great. Otherwise, synthesizing something
> like a VMR in some fashion may represent the best of both worlds.
> After all, your choice of filesystem format really doesn't matter as much as what you
> write to it.
> Future of Version Control
> Google isn't the only organization to publicly discuss the benefits of a monorepo
> approach. Microsoft, Facebook, Netflix, and Uber have also publicly mentioned their
> reliance on the approach. DORA has published about it extensively. It's vaguely possi‐
> ble that all of these successful, long-lived companies are misguided, or at least that
> their situations are sufficiently different as to be inapplicable to the average smaller
> organization. Although it's possible, we think it is unlikely.
> Most arguments against monorepos focus on the technical limitations of having a
> single large repository. If cloning a repository from upstream is quick and cheap,
> developers are more likely to keep changes small and isolated (and to avoid making
> 346
> |
> Chapter 16: Version Control and Branch Management

**ابزارهای مهندسی نرم‌افزار مدرن و Monorepo**

ابزارهای مهندسی نرم‌افزار شامل VCS و سیستم‌های build، به طور فزاینده مکانیزم‌هایی برای ترکیب هوشمندانه بین مخزن‌های ریزدانه (Fine-grained Repositories) و monorepoها ارائه می‌دهند تا تجربه‌ای شبیه monorepo فراهم کنند — ترتیب توافق شده‌ای از commitها و درک نمودار وابستگی. Git submodules، Bazel با وابستگی‌های خارجی و CMake subprojects همگی به توسعه‌دهندگان مدرن اجازه می‌دهند چیزی را که رفتار monorepo را به طور ضعیف تقریب می‌زند، بدون هزینه‌ها و معایب monorepo ترکیب کنند.

به عنوان مثال، مخزن‌های ریزدانه از نظر مقیاس آسان‌تر قابل مدیریت هستند (Git اغلب مشکلات عملکردی پس از چند میلیون commit دارد و تمایل دارد هنگام clone کردن مخزن‌هایی که شامل artifactهای binary بزرگ هستند، کند باشد) و storage (متاداده VCS می‌تواند جمع شود، به خصوص اگر artifactهای binary در سیستم کنترل نسخه خود دارید). مخزن‌های ریزدانه در یک مخزن با سبک federated/virtual-monorepo (VMR) می‌توانند جداسازی پروژه‌های آزمایشی یا فوق‌سری را آسان‌تر کنند و در عین حال به One Version پایبند بمانند و امکان دسترسی به ابزارهای مشترک را فراهم کنند.

**آینده کنترل نسخه**
گوگل تنها سازمانی نیست که به طور عمومی درباره مزایای رویکرد monorepo بحث کرده. Microsoft، Facebook، Netflix و Uber نیز به طور عمومی به وابستگی خود به این رویکرد اشاره کرده‌اند. DORA به طور گسترده درباره آن منتشر کرده. احتمال مبهمی وجود دارد که همه این شرکت‌های موفق و قدیمی نادرست راهنمایی شده باشند، یا حداقل اینکه شرایط آن‌ها به اندازه کافی متفاوت باشد که برای سازمان‌های کوچکتر متوسط قابل اعمال نباشد. اگرچه ممکن است، ما فکر می‌کنیم بعید است.

بیشتر استدلال‌ها علیه monorepoها روی محدودیت‌های فنی داشتن یک مخزن بزرگ واحد تمرکز دارند. اگر clone کردن یک مخزن از upstream سریع و ارزان باشد، توسعه‌دهندگان بیشتر احتمال دارد تغییرات را کوچک و جدا نگه دارند (و از ایجاد


![Section](images/page005-373.png)

![Section](images/page006-374.png)

![Section](images/page007-375.png)

![Section](images/page008-376.png)

---

###### 📄 صفحه ۳۷۷

**آینده کنترل نسخه ( ادامه)**

Monorepo در مقابل Multirepo یکی از بحث‌های داغ در مهندسی نرم‌افزار است. هر رویکرد مزایا و معایب خود را دارد:

**مزایای Monorepo:**
- اشتراک‌گذاری آسان کد بین پروژه‌ها
- تغییرات اتمیک در سراسر کد
- سادگی مدیریت وابستگی‌ها
- امکان refactor در سراسر کد

**معایب Monorepo:**
- مقیاس‌پذیری محدود
- زمان clone طولانی
- پیچیدگی build
- نیاز به ابزارهای تخصصی

**مزایای Multirepo:**
- مقیاس‌پذیری بهتر
- جداسازی پروژه‌ها
- سادگی ابزارها
- انعطاف‌پذیری بیشتر

**معایب Multirepo:**
- پیچیدگی مدیریت وابستگی‌ها
- دشواری refactor در سراسر کد
- نیاز به هماهنگی بیشتر بین تیم‌ها
- امکان ناسازگاری نسخه‌ها


![Section](images/page009-377.png)

![Section](images/page010-378.png)

![Section](images/page011-379.png)

![Section](images/page012-380-img1.png)

---

###### 📄 صفحه ۳۸۱
> within Google. Even older versions of the code can be referenced, so links can stay
> valid as the codebase evolves.
> What?
> Roughly one quarter of Code Searches are classic file browsing, to answer the ques‐
> tion of what a specific part of the codebase is doing. These kinds of tasks are usually
> more exploratory, rather than locating a specific result. This is using Code Search to
> read the source, to better understand code before making a change, or to be able to
> understand someone else's change.
> To ease these kinds of tasks, Code Search introduced browsing via call hierarchies
> and quick navigation between related files (e.g., between header, implementation, test,
> and build files). This is about understanding code by easily answering each of the
> many questions a developer has when looking at it.
> How?
> The most frequent use case—about one third of Code Searches—are about seeing
> examples of how others have done something. Typically, a developer has already
> found a specific API (e.g., how to read a file from remote storage) and wants to see
> how the API should be applied to a particular problem (e.g., how to set up the remote
> connection robustly and handle certain types of errors). Code Search is also used to
> find the proper library for specific problems in the first place (e.g., how to compute a
> fingerprint for integer values efficiently) and then pick the most appropriate imple‐
> mentation. For these kinds of tasks, a combination of searches and cross-reference
> browsing are typical.
> Why?
> Related to what code is doing, there are more targeted queries around why code is
> behaving differently than expected. About 16% of Code Searches try to answer the
> question of why a certain piece of code was added, or why it behaves in a certain way.
> Such questions often arise during debugging; for example, why does an error occur
> under these particular circumstances?
> An important capability here is being able to search and explore the exact state of the
> codebase at a particular point in time. When debugging a production issue, this can
> mean working with a state of the codebase that is weeks or months old, while debug‐
> ging test failures for new code usually means working with changes that are only
> minutes old. Both are possible with Code Search.
> 354
> |
> Chapter 17: Code Search

**Code Search در عمل**

در گوگل، Code Search ابزاری حیاتی برای درک و ناوبری codebase عظیم است. حتی نسخه‌های قدیمی‌تر کد نیز قابل مرجع هستند، بنابراین لینک‌ها می‌توانند با تکامل codebase معتبر باقی بمانند.

**چه چیزی؟**
تقریباً یک چهارم جستجوهای کد، مرور کلاسیک فایل است، برای پاسخ به این سؤال که بخش خاصی از codebase چه کاری انجام می‌دهد. این نوع وظایف معمولاً بیشتر اکتشافی هستند تا یافتن یک نتیجه خاص. این استفاده از Code Search برای خواندن سورس، درک بهتر کد قبل از ایجاد تغییر، یا درک تغییرات دیگران است.

برای تسهیل این نوع وظایف، Code Search مرور از طریق call hierarchies (سلسله‌مراتب فراخوانی) و ناوبری سریع بین فایل‌های مرتبط (مثلاً بین فایل‌های header، implementation، test و build) را معرفی کرد. این درباره درک کد با پاسخ آسان به هر یک از سؤالات زیادی است که یک توسعه‌دهنده هنگام نگاه کردن به کد دارد.

**چگونه؟**
بیشترین مورد استفاده — حدود یک سوم جستجوهای کد — درباره دیدن نمونه‌هایی از نحوه انجام کار توسط دیگران است. معمولاً، یک توسعه‌دهنده قبلاً یک API خاص پیدا کرده (مثلاً نحوه خواندن فایل از storage از راه دور) و می‌خواهد ببیند چگونه API باید در یک مشکل خاص اعمال شود (مثلاً نحوه راه‌اندازی اتصال از راه دور به صورت قوی و مدیریت انواع خاصی از خطاها). Code Search همچنین برای یافتن کتابخانه مناسب برای مشکلات خاص در وهله اول استفاده می‌شود (مثلاً نحوه محاسبه fingerprint برای مقادیر integer به صورت کارآمد) و سپس انتخاب مناسب‌ترین پیاده‌سازی.

**چرا؟**
مرتبط با اینکه کد چه کاری انجام می‌دهد، queryهای هدفمندتری درباره اینکه چرا کد متفاوت از انتظار رفتار می‌کند وجود دارد. حدود ۱۶٪ از جستجوهای کد سعی می‌کنند به این سؤال پاسخ دهند که چرا یک قطعه کد خاص اضافه شده، یا چرا به شکل خاصی رفتار می‌کند. چنین سؤالاتی اغلب در حین debug کردن ظاهر می‌شوند؛ به عنوان مثال، چرا خطا تحت این شرایط خاص رخ می‌دهد؟

توانایی مهم اینجا توانایی جستجو و کاوش state دقیق codebase در یک زمان خاص است. هنگام debug کردن یک مشکل production، این می‌تواند به معنای کار با state codebaseای باشد که هفته‌ها یا ماه‌ها قدیمی است، در حالی که debug کردن شکست تست‌ها برای کد جدید معمولاً به معنای کار با تغییراتی است که فقط چند دقیقه قدیمی هستند. هر دو با Code Search امکان‌پذیر هستند.


![Section](images/page013-381.png)

![Section](images/page014-382.png)

![Section](images/page015-383.png)

![Section](images/page016-384.png)

---

###### 📄 صفحه ۳۸۵
> Figure 17-3. Code Search integration in stack frames
> Compilation errors and tests also typically refer back to a code location (e.g., test X in
> file at line). These can be linkified even for unsubmitted code given that most devel‐
> opment happens in specific cloud-visible workspaces that are accessible and searcha‐
> ble by Code Search.
> Finally, codelabs and other documentation refer to APIs, examples, and implementa‐
> tions. Such links can be search queries referencing a specific class or function, which
> remain valid when the file structure changes. For code snippets, the most recent
> implementation at head can easily be embedded into a documentation page, as
> demonstrated in Figure 17-4, without the need to pollute the source file with addi‐
> tional documentation markers.
> Figure 17-4. Code Search integration in documentation
> 358
> |
> Chapter 17: Code Search

**ادغام Code Search با سایر ابزارها**

Code Search با ابزارهای مختلف توسعه ادغام شده تا تجربه توسعه‌دهنده را بهبود بخشد:

**ادغام با stack frames**
خطاهای کامپایل و تست‌ها نیز معمولاً به یک مکان کد ارجاع می‌دهند (مثلاً test X در file در خط Y). اینها حتی برای کد ارسال نشده (unsubmitted) نیز قابل لینک شدن هستند، با توجه به اینکه بیشتر توسعه در workspaceهای خاصی که توسط cloud قابل مشاهده هستند انجام می‌شود و توسط Code Search قابل دسترسی و جستجو هستند.

**ادغام با مستندات**
Codelabs و مستندات دیگر به APIها، نمونه‌ها و پیاده‌سازی‌ها ارجاع می‌دهند. چنین لینک‌هایی می‌توانند queryهای جستجو باشند که به یک کلاس یا تابع خاص ارجاع می‌دهند و وقتی ساختار فایل تغییر می‌کند، معتبر باقی می‌مانند. برای code snippets، آخرین پیاده‌سازی در head می‌تواند به راحتی در یک صفحه مستندات تعبیه شود، بدون نیاز به آلوده کردن فایل سورس با نشانگرهای مستندات اضافی.

**مزایای ادغام Code Search:**
- **دسترسی سریع**: توسعه‌دهندگان می‌توانند به سرعت کد مرتبط را پیدا کنند
- **حفظ context**: نیاز به جابجایی بین ابزارها کاهش می‌یابد
- **دقت بیشتر**: لینک‌ها دقیق و به روز هستند
- **کارایی بالاتر**: توسعه‌دهندگان زمان کمتری را صرف جستجو می‌کنند


![Section](images/page017-385-img1.png)

![Section](images/page018-386-img1.png)

![Section](images/page018-386-img2.png)

![Section](images/page019-387.png)

![Section](images/page020-388.png)

![Section](images/page021-389.png)

![Section](images/page022-390.png)

---