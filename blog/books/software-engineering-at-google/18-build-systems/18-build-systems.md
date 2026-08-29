> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۳۹۱
> 14 In programming languages, a symbol such as a function "Alert" often is defined in a particular scope, such as
> a class ("Monitor") or namespace ("absl"). The qualified name might then be absl::Monitor::Alert, and this is
> findable, even if it doesn't occur in the actual text.
> dependencies (library/module level references) and down to functions and classes.
> This global relevance is often referred to as the document's "priority."
> When using references for ranking, one must be aware of two challenges. First, you
> must be able to extract reference information reliably. In the early days, Google's
> Code Search extracted include/import statements with simple regular expressions
> and then applied heuristics to convert them into full file paths. With the growing
> complexity of a codebase, such heuristics became error prone and challenging to
> maintain. Internally, we replaced this part with correct information from the Kythe
> graph.
> Large-scale refactorings, such as open sourcing core libraries, present a second chal‐
> lenge. Such changes don't happen atomically in a single code update; rather, they need
> to be rolled out in multiple stages. Typically, indirections are introduced, hiding, for
> example, the move of files from usages. These kinds of indirections reduce the page
> rank of moved files and make it more difficult for developers to discover the new
> location. Additionally, file views usually become lost when files are moved, making
> the situation even worse. Because such global restructurings of the codebase are com‐
> paratively rare (most interfaces move rarely), the simplest solution is to manually
> boost files during such transition periods. (Or wait until the migration completes and
> for the natural processes to up-rank the file in its new location.)
> Query dependent signals
> Query independent signals can be computed offline, so computational cost isn't a
> major concern, although it can be high. For example, for the "page" rank, the signal
> depends on the whole corpus and requires a MapReduce-like batch processing to cal‐
> culate. Query dependent signals, which must be calculated for each query, should be
> cheap to compute. This means that they are restricted to the query and information
> quickly accessible from the index.
> Unlike web search, we don't just match on tokens. However, if there are clean token
> matches (that is, the search term matches with content with some form of breaks,
> such as whitespace, around it), a further boost is applied and case sensitivity is con‐
> sidered. This means, for example, a search for "Point" will score higher against "Point
> *p" than against "appointed to the council."
> For convenience, a default search matches filename and qualified symbols14 in addi‐
> tion to the actual file content. A user can specify the particular kind of match, but
> they don't need to. The scoring boosts symbol and filename matches over normal
> 364
> |
> Chapter 17: Code Search

**سیگنال‌های وابسته به Query و Independent از Query**

برای رتبه‌بندی نتایج جستجو، Code Search از سیگنال‌های مختلفی استفاده می‌کند:

**سیگنال‌های Independent از Query**
سیگنال‌های independent از query را می‌توان به صورت آفلاین محاسبه کرد، بنابراین هزینه محاسباتی نگرانی اصلی نیست، اگرچه می‌تواند بالا باشد. به عنوان مثال، برای "page" rank، سیگنال به کل مجموعه بستگی دارد و به پردازش batch شبیه MapReduce نیاز دارد تا محاسبه شود.

**سیگنال‌های وابسته به Query**
سیگنال‌های وابسته به query که باید برای هر query محاسبه شوند، باید ارزان محاسبه شوند. این به این معنی است که به query و اطلاعاتی که به سرعت از index قابل دسترسی هستند، محدود می‌شوند.

**تطبیق Token**
برخلاف جستجوی وب، ما فقط روی tokenها تطبیق نمی‌دهیم. با این حال، اگر تطبیق‌های تمیز token وجود داشته باشد (یعنی عبارت جستجو با محتوا با نوعی جداکننده، مانند فاصله، در اطراف آن تطبیق یابد)، boost اضافی اعمال می‌شود و case sensitivity در نظر گرفته می‌شود. این به این معنی است که به عنوان مثال، جستجوی "Point" در مقابل "Point *p" امتیاز بالاتری نسبت به "appointed to the council" کسب می‌کند.

**تطبیق نماد و نام فایل**
برای راحتی، جستجوی پیش‌فرض علاوه بر محتوای واقعی فایل، نام فایل و نمادهای qualified را نیز تطبیق می‌دهد. کاربر می‌تواند نوع خاص تطبیق را مشخص کند، اما نیازی به این کار ندارد. امتیازدهی، تطبیق‌های نماد و نام فایل را نسبت به تطبیق‌های عادی افزایش می‌دهد.


![Section](images/page001-391.png)

![Section](images/page002-392.png)

![Section](images/page003-393.png)

![Section](images/page004-394.png)

![Section](images/page005-395.png)

---

###### 📄 صفحه ۳۹۶
> 17 There are other intermediate varieties, such as building a prefix/suffix index, but generally they provide less
> expressiveness in search queries while still having high complexity and indexing costs.
> 18 Russ Cox, "Regular Expression Matching with a Trigram Index or How Google Code Search Worked."
> Tokenization also typically doesn't care about the case of letters ("r" versus "R"), and
> will often blur words; for example, reducing "searching" and "searched" to the same
> stem token search. This lack of precision is a significant problem when searching
> code. Finally, tokenization makes it impossible to search on whitespace or other word
> delimiters (commas, parentheses), which can be very important in code.
> A next step up17 in searching power is full substring search in which any sequence of
> characters can be searched for. One fairly efficient way to provide this is via a
> trigram-based index.18 In its simplest form, the resulting index size is still much
> smaller than the original source code size. However, the small size comes at the cost
> of relatively low recall accuracy compared to other substring indices. This means
> slower queries because the nonmatches need to be filtered out of the result set. This is
> where a good compromise between index size, search latency, and resource consump‐
> tion must be found that depends heavily on codebase size, resource availability, and
> searches per second.
> If a substring index is available, it's easy to extend it to allow regular expression
> searches. The basic idea is to convert the regular expression automaton into a set of
> substring searches. This conversion is straightforward for a trigram index and can be
> generalized to other substring indices. Because there is no perfect regular expression
> index, it will always be possible to construct queries that result in a brute-force
> search. However, given that only a small fraction of user queries are complex regular
> expressions, in practice, the approximation via substring indices works very well.
> Conclusion
> Code Search grew from an organic replacement for grep into a central tool boosting
> developer productivity, leveraging Google's web search technology along the way.
> What does this mean for you, though? If you are on a small project that easily fits in
> your IDE, probably not much. If you are responsible for the productivity of engineers
> on a larger codebase, there are probably some insights to be gained.
> The most important one is perhaps obvious: understanding code is key to developing
> and maintaining it, and this means that investing in understanding code will yield
> dividends that might be difficult to measure, but are real. Every feature we added to
> Code Search was and is used by developers to help them in their daily work (admit‐
> tedly some more than others). Two of the most important features, Kythe integration
> (i.e., adding semantic code understanding) and finding working examples, are also
> the most clearly tied to understanding code (versus, for example, finding it, or seeing
> Conclusion
> |
> 369

**نتیجه‌گیری**

Code Search از یک جایگزین طبیعی برای grep به ابزاری مرکزی برای افزایش بهره‌وری توسعه‌دهنده رشد کرد و در این مسیر از فناوری جستجوی وب گوگل بهره برد. اما این برای شما چه معنایی دارد؟ اگر در پروژه کوچکی هستید که به راحتی در IDE شما جای می‌گیرد، احتمالاً زیاد نه. اگر مسئول بهره‌وری مهندسان در یک codebase بزرگتر هستید، احتمالاً بینش‌هایی برای کسب وجود دارد.

مهمترین شاید واضح باشد: درک کد کلید توسعه و نگهداری آن است و این به این معنی است که سرمایه‌گذاری در درک کد سودهایی به همراه خواهد داشت که ممکن است اندازه‌گیری آن‌ها دشوار باشد، اما واقعی هستند. هر feature که به Code Search اضافه کردیم، توسط توسعه‌دهندگان برای کمک به کار روزانه‌شان استفاده می‌شد (البته برخی بیشتر از دیگران). دو مورد از مهمترین features، ادغام Kythe (یعنی اضافه کردن درک semantic کد) و یافتن نمونه‌های کاری، همچنین واضح‌ترین ارتباط را با درک کد دارند (در مقابل، به عنوان مثال، یافتن آن، یا دیدن

**درس‌های کلیدی Code Search:**
- **سرعت**: جستجو باید سریع باشد تا توسعه‌دهندگان بتوانند به سرعت کد مرتبط را پیدا کنند
- **دقت**: نتایج باید دقیق و مرتبط باشند
- **یکپارچگی**: Code Search باید با سایر ابزارهای توسعه ادغام شود
- **پوشش کامل**: تمام کد باید قابل جستجو باشد
- **پشتیبانی از نسخه‌ها**: باید امکان جستجو در نسخه‌های مختلف کد وجود داشته باشد


![Section](images/page006-396.png)

![Section](images/page007-397.png)

![Section](images/page008-398.png)

![Section](images/page009-399.png)

![Section](images/page010-400.png)

---

###### 📄 صفحه ۴۰۱
> • It becomes tedious. As your system grows more complex, you begin spending
> almost as much time working on your build scripts as on real code. Debugging
> shell scripts is painful, with more and more hacks being layered on top of one
> another.
> • It's slow. To make sure you weren't accidentally relying on stale libraries, you have
> your build script build every dependency in order every time you run it. You
> think about adding some logic to detect which parts need to be rebuilt, but that
> sounds awfully complex and error prone for a script. Or you think about specify‐
> ing which parts need to be rebuilt each time, but then you're back to square one.
> • Good news: it's time for a release! Better go figure out all the arguments you need
> to pass to the jar command to make your final build. And remember how to
> upload it and push it out to the central repository. And build and push the docu‐
> mentation updates, and send out a notification to users. Hmm, maybe this calls
> for another script...
> • Disaster! Your hard drive crashes, and now you need to recreate your entire sys‐
> tem. You were smart enough to keep all of your source files in version control,
> but what about those libraries you downloaded? Can you find them all again and
> make sure they were the same version as when you first downloaded them? Your
> scripts probably depended on particular tools being installed in particular places
> —can you restore that same environment so that the scripts work again? What
> about all those environment variables you set a long time ago to get the compiler
> working just right and then forgot about?
> • Despite the problems, your project is successful enough that you're able to begin
> hiring more engineers. Now you realize that it doesn't take a disaster for the pre‐
> vious problems to arise—you need to go through the same painful bootstrapping
> process every time a new developer joins your team. And despite your best
> efforts, there are still small differences in each person's system. Frequently, what
> works on one person's machine doesn't work on another's, and each time it takes
> a few hours of debugging tool paths or library versions to figure out where the
> difference is.
> • You decide that you need to automate your build system. In theory, this is as sim‐
> ple as getting a new computer and setting it up to run your build script every
> night using cron. You still need to go through the painful setup process, but now
> you don't have the benefit of a human brain being able to detect and resolve
> minor problems. Now, every morning when you get in, you see that last night's
> build failed because yesterday a developer made a change that worked on their
> system but didn't work on the automated build system. Each time it's a simple fix,
> but it happens so often that you end up spending a lot of time each day discover‐
> ing and applying these simple fixes.
> 374
> |
> Chapter 18: Build Systems and Build Philosophy

**مشکلات سیستم build دستی**

همان‌طور که سیستم شما پیچیده‌تر می‌شود، مشکلات زیادی با سیستم build دستی ظاهر می‌شوند:

- **کسل‌کننده می‌شود.** همان‌طور که سیستم شما پیچیده‌تر می‌شود، شروع به صرف تقریباً همان اندازه زمان روی اسکریپت‌های build خود می‌کنید تا روی کد واقعی. دیباگ کردن اسکریپت‌های shell دردناک است و هک‌های بیشتر و بیشتری روی یکدیگر انباشته می‌شوند.

- **کند است.** برای اطمینان از اینکه به طور تصادفی به کتابخانه‌های قدیمی وابسته نیستید، اسکریپت build خود را مجبور می‌کنید هر بار که اجرا می‌کنید هر وابستگی را به ترتیب build کند. فکر می‌کنید منطقی اضافه کنید تا تشخیص دهد کدام بخش‌ها نیاز به rebuild دارند، اما این برای یک اسکریپت بسیار پیچیده و مستعد خطا به نظر می‌رسد. یا فکر می‌کنید مشخص کنید هر بار کدام بخش‌ها نیاز به rebuild دارند، اما آنگاه به نقطه اول بازمی‌گردید.

- **فاجعه! هارد دیسک شما خراب می‌شود و حالا نیاز دارید سیستم کامل خود را بازسازی کنید.** شما هوشمندانه تمام فایل‌های سورس خود را در کنترل نسخه نگهداری کردید، اما درباره کتابخانه‌هایی که دانلود کردید چطور؟ آیا می‌توانید دوباره همه آن‌ها را پیدا کنید و مطمئن شوید همان نسخه‌ای بودند که اولین بار دانلود کردید؟ اسکریپت‌های شما احتمالاً به ابزارهای خاصی در مکان‌های خاص وابسته بودند — آیا می‌توانید همان محیط را بازیابی کنید تا اسکریپت‌ها دوباره کار کنند؟ درباره تمام آن environment variableهایی که مدت‌ها پیش تنظیم کردید تا کامپایلر درست کار کند و سپس فراموش کردید چطور؟

- **تصمیم می‌گیرید سیستم build خود را خودکار کنید.** در تئوری، این به اندازه گرفتن یک کامپیوتر جدید و پیکربندی آن برای اجرای اسکریپت build شما هر شب با استفاده از cron ساده است. هنوز نیاز دارید فرآیند دردناک setup را طی کنید، اما حالا مزیت مغز انسان در توانایی تشخیص و حل مشکلات جزئی را ندارید. حالا، هر صبح وقتی وارد می‌شوید، می‌بینید که build شب گذشته شکست خورده زیرا دیروز یک توسعه‌دهنده تغییری ایجاد کرد که روی سیستم خودش کار می‌کرد اما روی سیستم build خودکار کار نمی‌کرد. هر بار یک تعمیر ساده است، اما آنقدر اتفاق می‌افتد که در نهایت هر روز زمان زیادی صرف کشف و اعمال این تعمیرات ساده می‌کنید.


![Section](images/page011-401.png)

![Section](images/page012-402.png)

![Section](images/page013-403.png)

![Section](images/page014-404.png)

![Section](images/page015-405-img1.png)

---

###### 📄 صفحه ۴۰۶
> Difficulty performing incremental builds. A good build system will allow engineers to
> perform reliable incremental builds such that a small change doesn't require the
> entire codebase to be rebuilt from scratch. This is especially important if the build
> system is slow and unable to parallelize build steps for the aforementioned reasons.
> But unfortunately, task-based build systems struggle here, too. Because tasks can do
> anything, there's no way in general to check whether they've already been done. Many
> tasks simply take a set of source files and run a compiler to create a set of binaries;
> thus, they don't need to be rerun if the underlying source files haven't changed. But
> without additional information, the system can't say this for sure—maybe the task
> downloads a file that could have changed, or maybe it writes a timestamp that could
> be different on each run. To guarantee correctness, the system typically must rerun
> every task during each build.
> Some build systems try to enable incremental builds by letting engineers specify the
> conditions under which a task needs to be rerun. Sometimes this is feasible, but often
> it's a much trickier problem than it appears. For example, in languages like C++ that
> allow files to be included directly by other files, it's impossible to determine the entire
> set of files that must be watched for changes without parsing the input sources. Engi‐
> neers will often end up taking shortcuts, and these shortcuts can lead to rare and
> frustrating problems where a task result is reused even when it shouldn't be. When
> this happens frequently, engineers get into the habit of running clean before every
> build to get a fresh state, completely defeating the purpose of having an incremental
> build in the first place. Figuring out when a task needs to be rerun is surprisingly sub‐
> tle, and is a job better handled by machines than humans.
> Difficulty maintaining and debugging scripts. Finally, the build scripts imposed by task-
> based build systems are often just difficult to work with. Though they often receive
> less scrutiny, build scripts are code just like the system being built, and are easy places
> for bugs to hide. Here are some examples of bugs that are very common when work‐
> ing with a task-based build system:
> • Task A depends on task B to produce a particular file as output. The owner of
> task B doesn't realize that other tasks rely on it, so they change it to produce out‐
> put in a different location. This can't be detected until someone tries to run task
> A and finds that it fails.
> • Task A depends on task B, which depends on task C, which is producing a partic‐
> ular file as output that's needed by task A. The owner of task B decides that it
> doesn't need to depend on task C any more, which causes task A to fail even
> though task B doesn't care about task C at all!
> • The developer of a new task accidentally makes an assumption about the
> machine running the task, such as the location of a tool or the value of particular
> Modern Build Systems
> |
> 379

**سیستم‌های Build مدرن: مشکلات سیستم‌های مبتنی بر Task**

**دشواری انجام buildهای incremental**
یک سیستم build خوب به مهندسان اجازه می‌دهد buildهای incremental قابل اعتماد انجام دهند به طوری که یک تغییر کوچک نیاز به rebuild کل codebase از ابتدا نداشته باشد. این به خصوص اگر سیستم build کند باشد و قادر به موازی‌سازی مراحل build به دلایل ذکر شده نباشد، مهم است. اما متأسفانه، سیستم‌های build مبتنی بر task نیز اینجا مشکل دارند. چون taskها می‌توانند هر کاری انجام دهند، به طور کلی راهی برای بررسی اینکه آیا قبلاً انجام شده‌اند وجود ندارد. بسیاری از taskها صرفاً مجموعه‌ای از فایل‌های سورس را می‌گیرند و کامپایلر را اجرا می‌کنند تا مجموعه‌ای از binaryها ایجاد کنند؛ بنابراین، اگر فایل‌های سورس زیرین تغییر نکرده باشند، نیازی به اجرای مجدد ندارند. اما بدون اطلاعات اضافی، سیستم نمی‌تواند این را با اطمینان بگوید — شاید task فایلی را دانلود کند که ممکن است تغییر کرده باشد، یا شاید timestampی بنویسد که ممکن است در هر اجرا متفاوت باشد. برای تضمین درستی، سیستم معمولاً باید هر task را در هر build مجدداً اجرا کند.

برخی سیستم‌های build سعی می‌کنند buildهای incremental را با اجازه دادن به مهندسان برای مشخص کردن شرایطی که task باید مجدداً اجرا شود، فعال کنند. گاهی اوقات این عملی است، اما اغلب مشکلی بسیار پیچیده‌تر از آنچه به نظر می‌رسد است. به عنوان مثال، در زبان‌هایی مانند C++ که اجازه include شدن مستقیم فایل‌ها توسط فایل‌های دیگر را می‌دهند، بدون parse کردن سورس‌های ورودی، تعیین مجموعه کامل فایل‌هایی که باید تغییراتشان رصد شود، غیرممکن است.

**دشواری نگهداری و دیباگ کردن اسکریپت‌ها**
در نهایت، اسکریپت‌های build که توسط سیستم‌های build مبتنی بر task اعمال می‌شوند، اغلب به سختی قابل کار هستند. اگرچه اغلب بررسی کمتری دریافت می‌کنند، اسکریپت‌های build دقیقاً مانند سیستم در حال build کردن کد هستند و مکان‌های آسانی برای پنهان شدن باگ‌ها هستند. در اینجا چند مثال از باگ‌هایی که هنگام کار با سیستم build مبتنی بر task بسیار رایج هستند، آورده شده:

- Task A به Task B وابسته است تا فایل خاصی به عنوان خروجی تولید کند. مالک Task B متوجه نمی‌شود که سایر taskها به آن وابسته هستند، بنابراین آن را تغییر می‌دهد تا خروجی در مکان متفاوتی تولید شود. این تا زمانی که کسی سعی نکند task A را اجرا کند و متوجه شکست آن شود، قابل تشخیص نیست.

- Task A به Task B وابسته است که به Task C وابسته است که فایل خاصی به عنوان خروجی تولید می‌کند که برای Task A لازم است. مالک Task B تصمیم می‌گیرد دیگر به Task C وابسته نباشد، که باعث شکست Task A می‌شود حتی اگر Task B اصلاً به Task C اهمیت ندهد!

- توسعه‌دهنده یک task جدید تصادفاً فرضی درباره ماشین در حال اجرای task می‌سازد، مانند مکان یک ابزار یا مقدار خاصی


![Section](images/page016-406.png)

![Section](images/page017-407.png)

![Section](images/page018-408.png)

![Section](images/page019-409.png)

![Section](images/page020-410.png)

---

###### 📄 صفحه ۴۱۱
> workspace level. Whenever Blaze builds a java_library, it checks to make sure that
> the specified compiler is available at a known location and downloads it if not. Just
> like any other dependency, if the Java compiler changes, every artifact that was depen‐
> dent upon it will need to be rebuilt. Every type of target defined in Bazel uses this
> same strategy of declaring the tools it needs to run, ensuring that Bazel is able to
> bootstrap them no matter what exists on the system where it runs.
> Bazel solves the second part of the problem, platform independence, by using tool‐
> chains. Rather than having targets depend directly on their tools, they actually
> depend on types of toolchains. A toolchain contains a set of tools and other proper‐
> ties defining how a type of target is built on a particular platform. The workspace can
> define the particular toolchain to use for a toolchain type based on the host and target
> platform. For more details, see the Bazel manual.
> Extending the build system. Bazel comes with targets for several popular programming
> languages out of the box, but engineers will always want to do more—part of the ben‐
> efit of task-based systems is their flexibility in supporting any kind of build process,
> and it would be better not to give that up in an artifact-based build system. Fortu‐
> nately, Bazel allows its supported target types to be extended by adding custom rules.
> To define a rule in Bazel, the rule author declares the inputs that the rule requires (in
> the form of attributes passed in the BUILD file) and the fixed set of outputs that the
> rule produces. The author also defines the actions that will be generated by that rule.
> Each action declares its inputs and outputs, runs a particular executable or writes a
> particular string to a file, and can be connected to other actions via its inputs and out‐
> puts. This means that actions are the lowest-level composable unit in the build system
> —an action can do whatever it wants so long as it uses only its declared inputs and
> outputs, and Bazel will take care of scheduling actions and caching their results as
> appropriate.
> The system isn't foolproof given that there's no way to stop an action developer from
> doing something like introducing a nondeterministic process as part of their action.
> But this doesn't happen very often in practice, and pushing the possibilities for abuse
> all the way down to the action level greatly decreases opportunities for errors. Rules
> supporting many common languages and tools are widely available online, and most
> projects will never need to define their own rules. Even for those that do, rule defini‐
> tions only need to be defined in one central place in the repository, meaning most
> engineers will be able to use those rules without ever having to worry about their
> implementation.
> Isolating the environment. Actions sound like they might run into the same problems
> as tasks in other systems—isn't it still possible to write actions that both write to the
> same file and end up conflicting with one another? Actually, Bazel makes these
> conflicts impossible by using sandboxing. On supported systems, every action is iso‐
> 384
> |
> Chapter 18: Build Systems and Build Philosophy

**ابزارهای Build مدرن: Bazel**

Bazel سیستم build مدرنی است که توسط گوگل توسعه یافته و بسیاری از مشکلات سیستم‌های build مبتنی بر task را حل می‌کند. Bazel از مدل build مبتنی بر artifact استفاده می‌کند که در آن build بر اساس نتایج قابل تکرار (Reproducible) انجام می‌شود.

**تعریف toolchain و وابستگی‌ها**
Bazel ابزارها را به عنوان وابستگی مدیریت می‌کند. هر زمان Bazel یک java_library build می‌کند، بررسی می‌کند که کامپایلر مشخص شده در مکان شناخته‌شده در دسترس باشد و اگر نباشد، آن را دانلود می‌کند. درست مانند هر وابستگی دیگری، اگر کامپایلر Java تغییر کند، هر artifactی که به آن وابسته بوده نیاز به rebuild دارد. هر نوع target تعریف شده در Bazel از همین استراتژی اعلام ابزارهایی که برای اجرا نیاز دارد، استفاده می‌کند و تضمین می‌کند Bazel بتواند آن‌ها را bootstrap کند، صرف نظر از اینکه روی سیستمی که اجرا می‌شود چه چیزی وجود دارد.

**گسترش سیستم build**
Bazel با targets برای چندین زبان برنامه‌نویسی محبوب از جعبه خارج می‌شود، اما مهندسان همیشه می‌خواهند بیشتر کار کنند — بخشی از مزیت سیستم‌های مبتنی بر task انعطاف‌پذیری آن‌ها در پشتیبانی از هر نوع فرآیند build است و بهتر است این را در یک سیستم build مبتنی بر artifact رها نکنیم. خوشبختانه، Bazel اجازه می‌دهد انواع target پشتیبانی شده آن با اضافه کردن ruleهای سفارشی گسترش یابد.

برای تعریف یک rule در Bazel، نویسنده rule ورودی‌هایی را که rule نیاز دارد (به شکل attributeهایی که در فایل BUILD پاس داده می‌شوند) و مجموعه ثابتی از خروجی‌هایی که rule تولید می‌کند را اعلام می‌کند. نویسنده همچنین actionهایی را که توسط آن rule تولید می‌شوند، تعریف می‌کند. هر action ورودی‌ها و خروجی‌های خود را اعلام می‌کند، یک executable خاص را اجرا می‌کند یا رشته خاصی را در فایل می‌نویسد و می‌تواند از طریق ورودی‌ها و خروجی‌هایش به actionهای دیگر متصل شود. این به این معنی است که actionها کمترین واحد ترکیب‌پذیر در سیستم build هستند — یک action می‌تواند هر کاری انجام دهد تا زمانی که فقط از ورودی‌ها و خروجی‌های اعلام شده خود استفاده کند و Bazel از زمان‌بندی actionها و cache کردن نتایج آن‌ها به طور مناسب مراقبت می‌کند.

**جدا کردن محیط**
Actionها به نظر می‌رسد ممکن است با همان مشکلات taskها در سایر سیستم‌ها مواجه شوند — آیا هنوز امکان نوشتن actionهایی وجود ندارد که هر دو در یک فایل بنویسند و در نهایت با یکدیگر تداخل داشته باشند؟ در واقع، Bazel این تداخلات را با استفاده از sandboxing غیرممکن می‌کند. در سیستم‌های پشتیبانی شده، هر action


![Section](images/page021-411.png)

![Section](images/page022-412.png)

![Section](images/page023-413.png)

![Section](images/page024-414.png)

![Section](images/page025-415-img1.png)

![Section](images/page026-416-img1.png)

![Section](images/page027-417-img1.png)

![Section](images/page028-418.png)

---