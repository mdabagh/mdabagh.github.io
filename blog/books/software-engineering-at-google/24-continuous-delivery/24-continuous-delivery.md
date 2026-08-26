> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۵۲۵
> been approved), so the end-to-end tests could be run there. The post-submit CI runs
> every two hours, grabbing the latest code and configuration from green head, creates
> an RC, and runs the same end-to-end test suite against it that is already run in dev.
> Lesson learned.    Faster feedback loops prevent problems in dev deploys:
> • Moving tests for different Takeout products from “after nightly deploy” to pre‐
> submit prevented 95% of broken servers from bad configuration and reduced
> nightly deployment failures by 50%.
> • Though end-to-end tests couldn’t be moved all the way to presubmit, they were
> still moved from “after nightly deploy” to “post-submit within two hours.” This
> effectively cut the “culprit set” by 12 times.
> Scenario #2: Indecipherable test logs
> Problem: As Takeout incorporated more Google products, it grew into a mature plat‐
> form that allowed product teams to insert plug-ins, with product-specific data-
> fetching code, directly into Takeout’s binary. For example, the Google Photos plug-in
> knows how to fetch photos, album metadata, and the like. Takeout expanded from its
> original “handful” of products to now integrate with more than 90.
> Takeout’s end-to-end tests dumped its failures to a log, and this approach didn’t scale
> to 90 product plug-ins. As more products integrated, more failures were introduced.
> Even though the team was running the tests earlier and more often with the addition
> of the post-submit CI, multiple failures would still pile up inside and were easy to
> miss. Going through these logs became a frustrating time sink, and the tests were
> almost always failing.
> What the team did.    The team refactored the tests into a dynamic, configuration-based
> suite (using a parameterized test runner) that reported results in a friendlier UI,
> clearly showing individual test results as green or red: no more digging through logs.
> They also made failures much easier to debug, most notably, by displaying failure
> information, with links to logs, directly in the error message. For example, if Takeout
> failed to fetch a file from Gmail, the test would dynamically construct a link that
> searched for that file’s ID in the Takeout logs and include it in the test failure message.
> This automated much of the debugging process for product plug-in engineers and
> required less of the Takeout team’s assistance in sending them logs, as demonstrated
> in Figure 23-3.
> 498
> |
> Chapter 23: Continuous Integration


![Section](images/page001-525.png)

![Section](images/page002-526.png)

---

###### 📄 صفحه ۵۲۷
> Remaining challenge.    Going forward, the burden of testing “all of Google” (obviously,
> this is an exaggeration, as most product problems are caught by their respective
> teams) grows as Takeout integrates with more products and as those products
> become more complex. Manual comparisons between this CI and prod are an expen‐
> sive use of the Build Cop’s time.
> Future improvement.    This presents an interesting opportunity to try hermetic testing
> with record/replay in Takeout’s post-submit CI. In theory, this would eliminate fail‐
> ures from backend product APIs surfacing in Takeout’s CI, which would make the
> suite more stable and effective at catching failures in the last two hours of Takeout
> changes—which is its intended purpose.
> Scenario #4: Keeping it green
> Problem: As the platform supported more product plug-ins, which each included
> end-to-end tests, these tests would fail and the end-to-end test suites were nearly
> always broken. The failures could not all be immediately fixed. Many were due to
> bugs in product plug-in binaries, which the Takeout team had no control over. And
> some failures mattered more than others—low-priority bugs and bugs in the test
> code did not need to block a release, whereas higher-priority bugs did. The team
> could easily disable tests by commenting them out, but that would make the failures
> too easy to forget about.
> One common source of failures: tests would break when product plug-ins were roll‐
> ing out a feature. For example, a playlist-fetching feature for the YouTube plug-in
> might be enabled for testing in dev for a few months before being enabled in prod.
> The Takeout tests only knew about one result to check, so that often resulted in the
> test needing to be disabled in particular environments and manually curated as the
> feature rolled out.
> What the team did.    The team came up with a strategic way to disable failing tests by
> tagging them with an associated bug and filing that off to the responsible team (usu‐
> ally a product plug-in team). When a failing test was tagged with a bug, the team’s
> testing framework would suppress its failure. This allowed the test suite to stay green
> and still provide confidence that everything else, besides the known issues, was pass‐
> ing, as illustrated in Figure 23-4.
> 500
> |
> Chapter 23: Continuous Integration


چالش‌های اصلی:
1. **تعارض الزامات**: وابستگی‌های مختلف ممکن است الزامات متفاوتی داشته باشند
2. **وابستگی‌های الماسی**: وقتی دو وابستگی به نسخه‌های مختلف یک کتابخانه نیاز دارند
3. **وارد کردن وابستگی‌ها**: نحوه وارد کردن کتابخانه‌های خارجی

![Section](images/page003-527-img1.png)

![Section](images/page004-528.png)

---

###### 📄 صفحه ۵۲۹
> Figure 23-5. Mean time to close bug, after fix submitted
> Lessons learned.    Disabling failing tests that can’t be immediately fixed is a practical
> approach to keeping your suite green, which gives confidence that you’re aware of all
> test failures. Also, automating the test suite’s maintenance, including rollout manage‐
> ment and updating tracking bugs for fixed tests, keeps the suite clean and prevents
> technical debt. In DevOps parlance, we could call the metric in Figure 23-5 MTTCU:
> mean time to clean up.
> Future improvement.    Automating the filing and tagging of bugs would be a helpful
> next step. This is still a manual and burdensome process. As mentioned earlier, some
> of our larger teams already do this.
> Further challenges.    The scenarios we’ve described are far from the only CI challenges
> faced by Takeout, and there are still more problems to solve. For example, we men‐
> tioned the difficulty of isolating failures from upstream services in “CI Challenges” on
> page 490. This is a problem that Takeout still faces with rare breakages originating
> with upstream services, such as when a security update in the streaming infrastruc‐
> ture used by Takeout’s “Drive folder downloads” API broke archive decryption when
> it deployed to production. The upstream services are staged and tested themselves,
> but there is no simple way to automatically check with CI if they are compatible with
> Takeout after they’re launched into production. An initial solution involved creating
> an “upstream staging” CI environment to test production Takeout binaries against
> the staged versions of their upstream dependencies. However, this proved difficult to
> maintain, with additional compatibility issues between staging and production
> versions.
> 502
> |
> Chapter 23: Continuous Integration


وعده‌های سازگاری به توسعه‌دهندگان کمک می‌کند تا بدانند آیا می‌توانند کتابخانه را ارتقا دهند یا نه.

![Section](images/page005-529-img1.png)

![Section](images/page006-530-img1.png)

---

###### 📄 صفحه ۵۳۱


گوگل از یک سیستم مدیریت وابستگی داخلی استفاده می‌کند که به آن اجازه می‌دهد وابستگی‌ها را به طور مؤثر مدیریت کند.

![Section](images/page007-531.png)

![Section](images/page008-532.png)

---

###### 📄 صفحه ۵۳۳
> time between “code complete” and user feedback minimizes the cost of work that is in
> progress.
> You get extraordinary outcomes by realizing that the launch never lands but that it
> begins a learning cycle where you then fix the next most important thing, measure how
> it went, fix the next thing, etc.—and it is never complete.
> —David Weekly, Former Google product manager
> At Google, the practices we describe in this book allow hundreds (or in some cases
> thousands) of engineers to quickly troubleshoot problems, to independently work on
> new features without worrying about the release, and to understand the effectiveness
> of new features through A/B experimentation. This chapter focuses on the key levers
> of rapid innovation, including managing risk, enabling developer velocity at scale,
> and understanding the cost and value trade-off of each feature you launch.
> Idioms of Continuous Delivery at Google
> A core tenet of Continuous Delivery (CD) as well as of Agile methodology is that
> over time, smaller batches of changes result in higher quality; in other words, faster is
> safer. This can seem deeply controversial to teams at first glance, especially if the pre‐
> requisites for setting up CD—for example, Continuous Integration (CI) and testing—
> are not yet in place. Because it might take a while for all teams to realize the ideal of
> CD, we focus on developing various aspects that deliver value independently en route
> to the end goal. Here are some of these:
> Agility
> Release frequently and in small batches
> Automation
> Reduce or remove repetitive overhead of frequent releases
> Isolation
> Strive for modular architecture to isolate changes and make troubleshooting eas‐
> ier
> Reliability
> Measure key health indicators like crashes or latency and keep improving them
> Data-driven decision making
> Use A/B testing on health metrics to ensure quality
> Phased rollout
> Roll out changes to a few users before shipping to everyone
> At first, releasing new versions of software frequently might seem risky. As your user‐
> base grows, you might fear the backlash from angry users if there are any bugs that
> you didn’t catch in testing, and you might quite simply have too much new code in
> 506
> |
> Chapter 24: Continuous Delivery


عوامل مهم:
1. **سازگاری**: آیا وابستگی با سایر وابستگی‌ها سازگار است؟
2. **امنیت**: آیا وابستگی امن است؟
3. **قابلیت اطمینان**: آیا وابستگی قابل اطمینان است؟
4. **نگهداری**: آیا وابستگی به طور منظم به‌روز می‌شود؟

![Section](images/page009-533.png)

![Section](images/page010-534.png)

![Section](images/page011-535.png)

![Section](images/page012-536.png)

---
