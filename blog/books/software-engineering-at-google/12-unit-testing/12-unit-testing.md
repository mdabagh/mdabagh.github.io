> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
-

###### 📄 صفحه ۲۵۱
> For more information on TAP and our CI philosophy, see
> Chapter 23.
> Whether you are considering our size, our monorepo, or the number of products we
> offer, Google’s engineering environment is complex. Every week it experiences mil‐
> lions of changing lines, billions of test cases being run, tens of thousands of binaries
> being built, and hundreds of products being updated—talk about complicated!
> The Pitfalls of a Large Test Suite
> As a codebase grows, you will inevitably need to make changes to existing code.
> When poorly written, automated tests can make it more difficult to make those
> changes. Brittle tests—those that over-specify expected outcomes or rely on extensive
> and complicated boilerplate—can actually resist change. These poorly written tests
> can fail even when unrelated changes are made.
> If you have ever made a five-line change to a feature only to find dozens of unrelated,
> broken tests, you have felt the friction of brittle tests. Over time, this friction can
> make a team reticent to perform necessary refactoring to keep a codebase healthy.
> The subsequent chapters will cover strategies that you can use to improve the robust‐
> ness and quality of your tests.
> Some of the worst offenders of brittle tests come from the misuse of mock objects.
> Google’s codebase has suffered so badly from an abuse of mocking frameworks that it
> has led some engineers to declare “no more mocks!” Although that is a strong state‐
> ment, understanding the limitations of mock objects can help you avoid misusing
> them.
> For more information on working effectively with mock objects,
> see Chapter 13.
> In addition to the friction caused by brittle tests, a larger suite of tests will be slower
> to run. The slower a test suite, the less frequently it will be run, and the less benefit it
> provides. We use a number of techniques to speed up our test suite, including paral‐
> lelizing execution and using faster hardware. However, these kinds of tricks are even‐
> tually swamped by a large number of individually slow test cases.
> Tests can become slow for many reasons, like booting significant portions of a sys‐
> tem, firing up an emulator before execution, processing large datasets, or waiting for
> disparate systems to synchronize. Tests often start fast enough but slow down as the
> 224
> |
> Chapter 11: Testing Overview


![Section](images/page001-251.png)

![Section](images/page002-252-img1.png)

![Section](images/page003-253.png)

![Section](images/page004-254.png)

![Section](images/page005-255.png)

---

###### 📄 صفحه ۲۵۶
> Over time, testing has become an integral part of Google’s engineering culture. We
> have myriad ways to reinforce its value to engineers across the company. Through a
> combination of training, gentle nudges, mentorship, and, yes, even a little friendly
> competition, we have created the clear expectation that testing is everyone’s job.
> Why didn’t we start by mandating the writing of tests?
> The Testing Grouplet had considered asking for a testing mandate from senior lead‐
> ership but quickly decided against it. Any mandate on how to develop code would be
> seriously counter to Google culture and likely slow the progress, independent of the
> idea being mandated. The belief was that successful ideas would spread, so the focus
> became demonstrating success.
> If engineers were deciding to write tests on their own, it meant that they had fully
> accepted the idea and were likely to keep doing the right thing—even if no one was
> compelling them to.
> The Limits of Automated Testing
> Automated testing is not suitable for all testing tasks. For example, testing the quality
> of search results often involves human judgment. We conduct targeted, internal stud‐
> ies using Search Quality Raters who execute real queries and record their impres‐
> sions. Similarly, it is difficult to capture the nuances of audio and video quality in an
> automated test, so we often use human judgment to evaluate the performance of tel‐
> ephony or video-calling systems.
> In addition to qualitative judgements, there are certain creative assessments at which
> humans excel. For example, searching for complex security vulnerabilities is some‐
> thing that humans do better than automated systems. After a human has discovered
> and understood a flaw, it can be added to an automated security testing system like
> Google’s Cloud Security Scanner where it can be run continuously and at scale.
> A more generalized term for this technique is Exploratory Testing. Exploratory Test‐
> ing is a fundamentally creative endeavor in which someone treats the application
> under test as a puzzle to be broken, maybe by executing an unexpected set of steps or
> by inserting unexpected data. When conducting an exploratory test, the specific
> problems to be found are unknown at the start. They are gradually uncovered by
> probing commonly overlooked code paths or unusual responses from the application.
> As with the detection of security vulnerabilities, as soon as an exploratory test discov‐
> ers an issue, an automated test should be added to prevent future regressions.
> The Limits of Automated Testing
> |
> 229


سیستم ساخت نقش مهمی در فرآیند توسعه نرم‌افزار دارد. سیستم ساخت خوب می‌تواند زمان ساخت را کاهش دهد و خطاها را کم کند.

![Section](images/page006-256.png)

![Section](images/page007-257.png)

![Section](images/page008-258.png)

![Section](images/page009-259.png)

![Section](images/page010-260.png)

---

###### 📄 صفحه ۲۶۱
> of abstraction. Google’s reliance on large-scale changes (described in Chapter 22)
> to do such refactorings makes this case particularly important for us.
> New features
> When an engineer adds new features or behaviors to an existing system, the sys‐
> tem’s existing behaviors should remain unaffected. The engineer must write new
> tests to cover the new behaviors, but they shouldn’t need to change any existing
> tests. As with refactorings, a change to existing tests when adding new features
> suggest unintended consequences of that feature or inappropriate tests.
> Bug fixes
> Fixing a bug is much like adding a new feature: the presence of the bug suggests
> that a case was missing from the initial test suite, and the bug fix should include
> that missing test case. Again, bug fixes typically shouldn’t require updates to
> existing tests.
> Behavior changes
> Changing a system’s existing behavior is the one case when we expect to have to
> make updates to the system’s existing tests. Note that such changes tend to be sig‐
> nificantly more expensive than the other three types. A system’s users are likely to
> rely on its current behavior, and changes to that behavior require coordination
> with those users to avoid confusion or breakages. Changing a test in this case
> indicates that we’re breaking an explicit contract of the system, whereas changes
> in the previous cases indicate that we’re breaking an unintended contract. Low-
> level libraries will often invest significant effort in avoiding the need to ever make
> a behavior change so as not to break their users.
> The takeaway is that after you write a test, you shouldn’t need to touch that test again
> as you refactor the system, fix bugs, or add new features. This understanding is what
> makes it possible to work with a system at scale: expanding it requires writing only a
> small number of new tests related to the change you’re making rather than potentially
> having to touch every test that has ever been written against the system. Only break‐
> ing changes in a system’s behavior should require going back to change its tests, and
> in such situations, the cost of updating those tests tends to be small relative to the cost
> of updating all of the system’s users.
> Test via Public APIs
> Now that we understand our goal, let’s look at some practices for making sure that
> tests don’t need to change unless the requirements of the system being tested change.
> By far the most important way to ensure this is to write tests that invoke the system
> being tested in the same way its users would; that is, make calls against its public API
> rather than its implementation details. If tests work the same way as the system’s
> users, by definition, change that breaks a test might also break a user. As an addi‐
> tional bonus, such tests can serve as useful examples and documentation for users.
> 234
> |
> Chapter 12: Unit Testing


ویژگی‌های سیستم ساخت خوب:
1. **سرعت**: ساخت باید سریع انجام شود
2. **قابلیت اطمینان**: ساخت باید قابل اطمینان باشد
3. **قابلیت تکرار**: ساخت باید قابل تکرار باشد
4. **مقیاس‌پذیری**: سیستم باید بتواند با افزایش حجم کار مقیاس پیدا کند

![Section](images/page011-261.png)

![Section](images/page012-262.png)

![Section](images/page013-263.png)

![Section](images/page014-264.png)

![Section](images/page015-265.png)

---

###### 📄 صفحه ۲۶۶
> 3 These are also the same two reasons that a test can be “flaky.” Either the system under test has a nondetermin‐
> istic fault, or the test is flawed such that it sometimes fails when it should pass.
> The most common reason for problematic interaction tests is an over reliance on
> mocking frameworks. These frameworks make it easy to create test doubles that
> record and verify every call made against them, and to use those doubles in place of
> real objects in tests. This strategy leads directly to brittle interaction tests, and so we
> tend to prefer the use of real objects in favor of mocked objects, as long as the real
> objects are fast and deterministic.
> For a more extensive discussion of test doubles and mocking
> frameworks, when they should be used, and safer alternatives, see
> Chapter 13.
> Writing Clear Tests
> Sooner or later, even if we’ve completely avoided brittleness, our tests will fail. Failure
> is a good thing—test failures provide useful signals to engineers, and are one of the
> main ways that a unit test provides value.
> Test failures happen for one of two reasons:3
> • The system under test has a problem or is incomplete. This result is exactly what
> tests are designed for: alerting you to bugs so that you can fix them.
> • The test itself is flawed. In this case, nothing is wrong with the system under test,
> but the test was specified incorrectly. If this was an existing test rather than one
> that you just wrote, this means that the test is brittle. The previous section dis‐
> cussed how to avoid brittle tests, but it’s rarely possible to eliminate them entirely.
> When a test fails, an engineer’s first job is to identify which of these cases the failure
> falls into and then to diagnose the actual problem. The speed at which the engineer
> can do so depends on the test’s clarity. A clear test is one whose purpose for existing
> and reason for failing is immediately clear to the engineer diagnosing a failure. Tests
> fail to achieve clarity when their reasons for failure aren’t obvious or when it’s difficult
> to figure out why they were originally written. Clear tests also bring other benefits,
> such as documenting the system under test and more easily serving as a basis for new
> tests.
> Test clarity becomes significant over time. Tests will often outlast the engineers who
> wrote them, and the requirements and understanding of a system will shift subtly as
> it ages. It’s entirely possible that a failing test might have been written years ago by an
> Writing Clear Tests
> |
> 239


با استفاده از منابع محاسباتی توزیع‌شده، می‌توان مراحل ساخت را به طور همزمان اجرا کرد و زمان ساخت را کاهش داد.

![Section](images/page016-266.png)

![Section](images/page017-267-img1.png)

![Section](images/page018-268.png)

![Section](images/page019-269.png)

![Section](images/page020-270.png)

---

###### 📄 صفحه ۲۷۱
> the “then” and “when” blocks in this way can make the test less clear because it makes
> it difficult to distinguish the action being performed from the expected result.
> When a test does want to validate each step in a multistep process, it’s acceptable to
> define alternating sequences of when/then blocks. Long blocks can also be made
> more descriptive by splitting them up with the word “and.” Example 12-12 shows
> what a relatively complex, behavior-driven test might look like.
> Example 12-12. Alternating when/then blocks within a test
> @Test
> public void shouldTimeOutConnections() {
> // Given two users
> User user1 = newUser();
> User user2 = newUser();
> // And an empty connection pool with a 10-minute timeout
> Pool pool = newPool(Duration.minutes(10));
> // When connecting both users to the pool
> pool.connect(user1);
> pool.connect(user2);
> // Then the pool should have two connections
> assertThat(pool.getConnections()).hasSize(2);
> // When waiting for 20 minutes
> clock.advance(Duration.minutes(20));
> // Then the pool should have no connections
> assertThat(pool.getConnections()).isEmpty();
> // And each user should be disconnected
> assertThat(user1.isConnected()).isFalse();
> assertThat(user2.isConnected()).isFalse();
> }
> When writing such tests, be careful to ensure that you’re not inadvertently testing
> multiple behaviors at the same time. Each test should cover only a single behavior,
> and the vast majority of unit tests require only one “when” and one “then” block.
> Name tests after the behavior being tested
> Method-oriented tests are usually named after the method being tested (e.g., a test for
> the updateBalance method is usually called testUpdateBalance). With more focused
> behavior-driven tests, we have a lot more flexibility and the chance to convey useful
> information in the test’s name. The test name is very important: it will often be the
> first or only token visible in failure reports, so it’s your best opportunity to communi‐
> 244
> |
> Chapter 12: Unit Testing


قوانین سYST ساخت به سیستم می‌گویند چگونه کد را بسازد. این قوانین باید شفاف و قابل درک باشند.

![Section](images/page021-271.png)

![Section](images/page022-272.png)

![Section](images/page023-273.png)

![Section](images/page024-274.png)

![Section](images/page025-275.png)

![Section](images/page026-276.png)

---
