> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۴۱۹
> Minimizing Module Visibility
> Bazel and other build systems allow each target to specify a visibility: a property that
> specifies which other targets may depend on it. Targets can be public, in which case
> they can be referenced by any other target in the workspace; private, in which case
> they can be referenced only from within the same BUILD file; or visible to only an
> explicitly defined list of other targets. A visibility is essentially the opposite of a
> dependency: if target A wants to depend on target B, target B must make itself visible
> to target A.
> Just like in most programming languages, it is usually best to minimize visibility as
> much as possible. Generally, teams at Google will make targets public only if those
> targets represent widely used libraries available to any team at Google. Teams that
> require others to coordinate with them before using their code will maintain a white‐
> list of customer targets as their target’s visibility. Each team’s internal implementation
> targets will be restricted to only directories owned by the team, and most BUILD files
> will have only one target that isn’t private.
> Managing Dependencies
> Modules need to be able to refer to one another. The downside of breaking a code‐
> base into fine-grained modules is that you need to manage the dependencies among
> those modules (though tools can help automate this). Expressing these dependencies
> usually ends up being the bulk of the content in a BUILD file.
> Internal dependencies
> In a large project broken into fine-grained modules, most dependencies are likely to
> be internal; that is, on another target defined and built in the same source repository.
> Internal dependencies differ from external dependencies in that they are built from
> source rather than downloaded as a prebuilt artifact while running the build. This
> also means that there’s no notion of “version” for internal dependencies—a target and
> all of its internal dependencies are always built at the same commit/revision in the
> repository.
> One issue that should be handled carefully with regard to internal dependencies is
> how to treat transitive dependencies (Figure 18-5). Suppose target A depends on target
> B, which depends on a common library target C. Should target A be able to use
> classes defined in target C?
> Figure 18-5. Transitive dependencies
> 392
> |
> Chapter 18: Build Systems and Build Philosophy


![Section](images/page001-419.png)

![Section](images/page002-420-img1.png)

![Section](images/page003-421.png)

![Section](images/page004-422.png)

---

###### 📄 صفحه ۴۲۳
> repository, and clients need to ensure that they stay up to date with the latest version.
> Debugging also becomes much more difficult because different parts of the system
> will have been built from different points in the repository, and there is no longer a
> consistent view of the source tree.
> A better way to solve the problem of artifacts taking a long time to build is to use a
> build system that supports remote caching, as described earlier. Such a build system
> will save the resulting artifacts from every build to a location that is shared across
> engineers, so if a developer depends on an artifact that was recently built by someone
> else, the build system will automatically download it instead of building it. This pro‐
> vides all of the performance benefits of depending directly on artifacts while still
> ensuring that builds are as consistent as if they were always built from the same
> source. This is the strategy used internally by Google, and Bazel can be configured to
> use a remote cache.
> Security and reliability of external dependencies.    Depending on artifacts from third-
> party sources is inherently risky. There’s an availability risk if the third-party source
> (e.g., an artifact repository) goes down, because your entire build might grind to a
> halt if it’s unable to download an external dependency. There’s also a security risk: if
> the third-party system is compromised by an attacker, the attacker could replace the
> referenced artifact with one of their own design, allowing them to inject arbitrary
> code into your build.
> Both problems can be mitigated by mirroring any artifacts you depend on onto
> servers you control and blocking your build system from accessing third-party arti‐
> fact repositories like Maven Central. The trade-off is that these mirrors take effort
> and resources to maintain, so the choice of whether to use them often depends on the
> scale of the project. The security issue can also be completely prevented with little
> overhead by requiring the hash of each third-party artifact to be specified in the
> source repository, causing the build to fail if the artifact is tampered with.
> Another alternative that completely sidesteps the issue is to vendor your project’s
> dependencies. When a project vendors its dependencies, it checks them into source
> control alongside the project’s source code, either as source or as binaries. This effec‐
> tively means that all of the project’s external dependencies are converted to internal
> dependencies. Google uses this approach internally, checking every third-party
> library referenced throughout Google into a third_party directory at the root of Goo‐
> gle’s source tree. However, this works at Google only because Google’s source control
> system is custom built to handle an extremely large monorepo, so vendoring might
> not be an option for other organizations.
> 396
> |
> Chapter 18: Build Systems and Build Philosophy


در ادغام مداوم، توسعه‌دهندگان تغییرات خود را به طور مکرر در شاخه اصلی ادغام می‌کنند. این به شناسایی سریع مشکلات و کاهش تعارضات کمک می‌کند.

![Section](images/page005-423.png)

![Section](images/page006-424.png)

![Section](images/page007-425.png)

![Section](images/page008-426.png)

---

###### 📄 صفحه ۴۲۷
> Simplicity
> Critique’s user interface (UI) is based around making it easy to do code review
> without a lot of unnecessary choices, and with a smooth interface. The UI loads
> fast, navigation is easy and hotkey supported, and there are clear visual markers
> for the overall state of whether a change has been reviewed.
> Foundation of trust
> Code review is not for slowing others down; instead, it is for empowering others.
> Trusting colleagues as much as possible makes it work. This might mean, for
> example, trusting authors to make changes and not requiring an additional
> review phase to double check that minor comments are actually addressed. Trust
> also plays out by making changes openly accessible (for viewing and reviewing)
> across Google.
> Generic communication
> Communication problems are rarely solved through tooling. Critique prioritizes
> generic ways for users to comment on the code changes, instead of complicated
> protocols. Critique encourages users to spell out what they want in their com‐
> ments or even suggests some edits instead of making the data model and process
> more complex. Communication can go wrong even with the best code review
> tool because the users are humans.
> Workflow integration
> Critique has a number of integration points with other core software develop‐
> ment tools. Developers can easily navigate to view the code under review in our
> code search and browsing tool, edit code in our web-based code editing tool, or
> view test results associated with a code change.
> Across these guiding principles, simplicity has probably had the most impact on the
> tool. There were many interesting features we considered adding, but we decided not
> to make the model more complicated to support a small set of users.
> Simplicity also has an interesting tension with workflow integration. We considered
> but ultimately decided against creating a “Code Central” tool with code editing,
> reviewing, and searching in one tool. Although Critique has many touchpoints with
> other tools, we consciously decided to keep code review as the primary focus. Fea‐
> tures are linked from Critique but implemented in different subsystems.
> Code Review Flow
> Code reviews can be executed at many stages of software development, as illustrated
> in Figure 19-1. Critique reviews typically take place before a change can be commit‐
> ted to the codebase, also known as precommit reviews. Although Chapter 9 contains a
> brief description of the code review flow, here we expand it to describe key aspects of
> 400
> |
> Chapter 19: Critique: Google’s Code Review Tool


اصول اصلی:
1. **اتوماسیون**: فرآیندها باید خودکار باشند
2. **بازخورد سریع**: بازخورد باید سریع ارائه شود
3. **تست مداوم**: تست‌ها باید به طور مداوم اجرا شوند
4. **عدم شکستن ساخت**: ساخت اصلی نباید شکسته شود

![Section](images/page009-427.png)

![Section](images/page010-428.png)

![Section](images/page011-429-img1.png)

![Section](images/page012-430.png)

---

###### 📄 صفحه ۴۳۱
> Users can also view the diff in various different modes, such as overlay and side by
> side. When developing Critique, we decided that it was important to have side-by-
> side diffs to make the review process easier. Side-by-side diffs take a lot of space: to
> make them a reality, we had to simplify the diff view structure, so there is no border,
> no padding—just the diff and line numbers. We also had to play around with a vari‐
> ety of fonts and sizes until we had a diff view that accommodates even for Java’s 100-
> character line limit for the typical screen-width resolution when Critique launched
> (1,440 pixels).
> Critique further supports a variety of custom tools that provide diffs of artifacts pro‐
> duced by a change, such as a screenshot diff of the UI modified by a change or con‐
> figuration files generated by a change.
> To make the process of navigating diffs smooth, we were careful not to waste space
> and spent significant effort ensuring that diffs load quickly, even for images and large
> files and/or changes. We also provide keyboard shortcuts to quickly navigate through
> files while visiting only modified sections.
> When users drill down to the file level, Critique provides a UI widget with a compact
> display of the chain of snapshot versions of a file; users can drag and drop to select
> which versions to compare. This widget automatically collapses similar snapshots,
> drawing focus to important snapshots. It helps the user understand the evolution of a
> file within a change; for example, which snapshots have test coverage, have already
> been reviewed, or have comments. To address concerns of scale, Critique prefetches
> everything, so loading different snapshots is very quick.
> Analysis Results
> Uploading a snapshot of the change triggers code analyzers (see Chapter 20). Critique
> displays the analysis results on the change page, summarized by analyzer status chips
> shown below the change description, as depicted in Figure 19-3, and detailed in the
> Analysis tab, as illustrated in Figure 19-4.
> Analyzers can mark specific findings to highlight in red for increased visibility. Ana‐
> lyzers that are still in progress are represented by yellow chips, and gray chips are dis‐
> played otherwise. For the sake of simplicity, Critique offers no other options to mark
> or highlight findings—actionability is a binary option. If an analyzer produces some
> results (“findings”), clicking the chip opens up the findings. Like comments, findings
> can be displayed inside the diff but styled differently to make them easily distinguish‐
> able. Sometimes, the findings also include fix suggestions, which the author can pre‐
> view and choose to apply from Critique.
> 404
> |
> Chapter 19: Critique: Google’s Code Review Tool


چالش‌های اصلی:
1. **محدودیت‌های منابع**: منابع محاسباتی محدود هستند
2. **زمان اجرا**: زمان اجرای تست‌ها ممکن است زیاد باشد
3. ** quản lý شکست‌ها**: شکست‌ها باید به درستی مدیریت شوند

![Section](images/page013-431-img1.png)

![Section](images/page014-432.png)

![Section](images/page015-433-img1.png)

![Section](images/page015-433-img2.png)

![Section](images/page016-434.png)

---

###### 📄 صفحه ۴۳۵
> Assigning a reviewer to a change triggers a review request. This request runs “presub‐
> mits” or precommit hooks applicable to the change; teams can configure the presub‐
> mits related to their projects in many ways. The most common hooks include the
> following:
> • Automatically adding email lists to changes to raise awareness and transparency
> • Running automated test suites for the project
> • Enforcing project-specific invariants on both code (to enforce local code style
> restrictions) and change descriptions (to allow generation of release notes or
> other forms of tracking)
> As running tests is resource intensive, at Google they are part of presubmits (run
> when requesting review and when committing changes) rather than for every snap‐
> shot like Tricorder checks. Critique surfaces the result of running the hooks in a simi‐
> lar way to how analyzer results are displayed, with an extra distinction to highlight
> the fact that a failed result blocks the change from being sent for review or commit‐
> ted. Critique notifies the author via email if presubmits fail.
> Stages 3 and 4: Understanding and Commenting on a
> Change
> After the review process starts, the author and the reviewers work in tandem to reach
> the goal of committing changes of high quality.
> Commenting
> Making comments is the second most common action that users make in Critique
> after viewing changes (Figure 19-6). Commenting in Critique is free for all. Anyone
> —not only the change author and the assigned reviewers—can comment on a change.
> Critique also offers the ability to track review progress via per-person state. Reviewers
> have checkboxes to mark individual files at the latest snapshot as reviewed, helping
> the reviewer keep track of what they have already looked at. When the author modi‐
> fies a file, the “reviewed” checkbox for that file is cleared for all reviewers because the
> latest snapshot has been updated.
> 408
> |
> Chapter 19: Critique: Google’s Code Review Tool


ویژگی‌های TAP:
1. **مدیریت شکست‌ها**: شناسایی و مدیریت شکست‌ها
2. **پیدا کردن مقصر**: شناسایی علت شکست
3. **بهینه‌سازی پیش‌ارسال**: بهینه‌سازی تست‌های پیش‌ارسال

![Section](images/page017-435-img1.png)

![Section](images/page018-436.png)

![Section](images/page019-437-img1.png)

![Section](images/page020-438-img1.png)

---
