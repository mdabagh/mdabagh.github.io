> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب/وب‌سایت به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: Docs Like Code — مستندات را مثل کد مدیریت کن

> **منبع اصلی:** Docs Like Code / Let's Treat Docs Like Code
> **نویسنده:** Anne Gentle
> **ویرایش:** ویرایش دوم کتاب (Lulu) + وب‌سایت آموزشی
> **لینک:** https://www.docslikecode.com/
> **نوع:** کتاب + وب‌سایت آموزشی (رایگان)

---

## چکیده

> Docs Like Code — A modern approach to technical documentation
> Ship better docs by treating them like code. Version control, automation, and real team collaboration — the same workflow developers already use, applied to technical documentation.

**Docs Like Code** رویکردی مدرن برای مستندسازی فنی است.
مستندات بهتر را منتشر کنید، با این کار که **آن‌ها را مثل کد مدیریت کنید**. کنترل نسخه، اتوماسیون و همکاری واقعی تیمی — همان گردش‌کاری که توسعه‌دهندگان از قبل با آن آشنا هستند، این بار اعمال‌شده بر مستندات فنی.

> Version control, automation, and real team collaboration — the same workflow developers already use, applied to technical documentation. This site and the book behind it show you exactly how.

این وب‌سایت و کتاب پشت آن، دقیقاً نشان می‌دهند چگونه این کار انجام می‌شود.

> 📘 Now in its Second Edition

کتاب اکنون در **ویرایش دوم** است.

---

## چهار ستون Docs Like Code

### ۱. نسخه‌بندی همهٔ تغییرات

> ### Version every change
> Use Git to track who changed what and why — for docs, not just code.

**همهٔ تغییرات را نسخه‌بندی کنید.**
از Git استفاده کنید تا مشخص باشد **چه کسی**، **چه چیزی** و **چرا** را تغییر داده — برای مستندات، نه فقط کد.

> **به زبان ساده:** اگر نمی‌دانید چه کسی یک جمله را در README عوض کرده و چرا، مستندات شما دوباره‌نویسی می‌شود. Git تاریخچهٔ تصمیم‌ها را نگه می‌دارد، نه فقط تاریخچهٔ متن را.

### ۲. خودکارسازی بیلد

> ### Automate your builds
> CI/CD pipelines that publish your docs on every merge, no manual steps.

**بیلدها را خودکار کنید.**
خطوط لولهٔ CI/CD که مستندات شما را در **هر merge** منتشر می‌کنند، بدون هیچ مرحلهٔ دستی.

> **مهم‌ترین خاصیت این مرحله:** نبودِ «مرحلهٔ دستی». هر مرحلهٔ دستی، نقطه‌ای است که مستندات از کد عقب می‌افتند.

### ۳. بازبینی با Pull Request

> ### Review with pull requests
> Writers and developers collaborate in the same workflow they already know.

**بازبینی با Pull Request انجام شود.**
نویسندگان و توسعه‌دهندگان در همان گردش‌کاری که از قبل می‌شناسند با هم همکاری می‌کنند.

> **مزیت اصلی:** چون بازبینی مستندات از مسیر آشنای PR می‌گذرد، دیگر به «مرحلهٔ تأیید» جداگانه و فراموش‌شده نیاز نیست.

### ۴. مقیاس‌پذیری با تیم

> ### Scale with your team
> Patterns that work whether you're a solo writer or a distributed doc team.

**با تیم مقیاس بگیرید.**
الگوهایی که چه یک نویسندهٔ مستقل داشته باشد و چه یک تیم مستندات توزیع‌شده.

---

## آزمایش عملی در کمتر از ۱۰ دقیقه

> ### Try it in your browser — under 10 minutes
> No local setup needed. All you need is a GitHub account.
> 1. Create a free GitHub account at github.com.
> 2. Create a new repository named `yourusername.github.io` — for example, `annegentle.github.io`.
> 3. On the repository's **Code** tab, click *Add file* → *Create new file*. Name the file `index.md` and add a line of text — this becomes your live web page.
> 4. Click *Commit new file*.
> 5. Wait a few seconds, then visit `https://yourusername.github.io`.

**در مرورگر خود امتحانش کنید — کمتر از ۱۰ دقیقه.**
نیازی به نصب چیزی نیست. فقط یک حساب GitHub لازم است.

۱. یک حساب رایگان GitHub بسازید.
۲. یک مخزن جدید با نام `yourusername.github.io` بسازید.
۳. در تب **Code**، روی *Add file* → *Create new file* کلیک کنید. فایل را `index.md` نام بگذارید و یک خط متن بنویسید — این می‌شود صفحهٔ زندهٔ شما.
۴. روی *Commit new file* کلیک کنید.
۵. چند ثانیه صبر کنید، سپس به `https://yourusername.github.io` سر بزنید.

> That's the core loop: write a file, commit it, and it publishes automatically.

این هستهٔ کار است: **یک فایل بنویس، commit کن، و به‌صورت خودکار منتشر می‌شود.**

> **نکتهٔ مهم:** این حلقه نشان می‌دهد چرا docs-as-code کار می‌کند. فاصلهٔ «ویرایش → انتشار» **صفر** می‌شود. وقتی فاصله صفر باشد، مستندات عقب نمی‌افتند. تمام بحث این کتاب در واقع بحث همین صفر کردن فاصله است.

---

## این کتاب برای چه کسی است؟

> **Technical Writers** Work alongside engineers without losing control of your docs.
> **Developer Advocates** Publish and maintain API docs that stay in sync with the code.
> **Engineering Teams** Adopt a lightweight docs workflow that fits your existing CI/CD setup.
> **Doc Team Leads** Build systems that don't break when headcount or tooling changes.

| نقش | چه چیزی می‌گیرد |
|---|---|
| **نویسندگان فنی** | کنار مهندسان کار می‌کنند، بدون از دست دادن کنترل مستندات |
| **مربیان توسعه‌دهنده** | مستندات API منتشر و نگهداری می‌کنند که با کد همگام می‌ماند |
| **تیم‌های مهندسی** | یک گردش‌کار سبک مستندات که با CI/CD موجود جور می‌شود |
| **سرپرست تیم مستندات** | سامانه‌ای می‌سازند که با تغییر نفرات یا ابزار نمی‌شکند |

> **کتاب برای چه کسی مناسب نیست:** کسانی که هیچ آشنایی با Git یا Markdown ندارند.

---

## چرا این کتاب اهمیت دارد؟

> Most documentation teams struggle with:
> - Siloed tools and workflows
> - Slow publishing cycles
> - Poor collaboration with engineering
> - Content that quickly becomes outdated

> Docs Like Code shows you how to fix this.

اکثر تیم‌های مستندات با این مشکلات دست‌وپنجه نرم می‌کنند:
- **ابزارها و گردش‌کارهای جزیره‌ای** (مستندات در Wiki، کد در Git، مشکل در Confluence)
- **چرخه‌های انتشار کند**
- **همکاری ضعیف با مهندسی**
- **محتوایی که به‌سرعت منسوخ می‌شود**

و با اعمال شیوه‌های توسعهٔ نرم‌افزار بر مستندات:

> By applying software development practices to documentation, you can:
> - Ship docs faster
> - Improve accuracy and consistency
> - Collaborate seamlessly with developers
> - Build a sustainable, scalable documentation system

- مستندات را **سریع‌تر** منتشر کنید
- **دقت و یکدستی** را بالا ببرید
- **بی‌وقفه** با توسعه‌دهندگان همکاری کنید
- یک سامانهٔ مستندات **پایدار و مقیاس‌پذیر** بسازید

---

## فهرست فصل‌های کتاب (ویرایش دوم)

> - **Why treat docs as code?** دلایل توجیه‌آمیز برای اعمال شیوه‌های توسعهٔ نرم‌افزار بر مستندات، از چرخهٔ سریع‌تر تا همکاری بهتر.
> - **Background for docs as code** تکامل شیوه‌های مستندسازی و نحوهٔ ظهور docs-as-code به‌عنوان پاسخ به چالش‌های رایج صنعت.
> - **Plan for docs as code** ارزیابی گردش‌کار فعلی مستندات و ساخت نقشهٔ راه راهبردی برای پذیرش docs-as-code.
> - **Automate builds so you can focus on writing** راه‌اندازی خط لولهٔ انتشار خودکار.
> - **Teamwork and GitHub workflows with docs-as-code systems** تسلط بر گردش‌کارهای همکاری با PR، review و هماهنگی تیم.
> - **Test the docs: linting, inclusive language, and DocOps** تضمین کیفیت با تست خودکار، بررسی دسترس‌پذیری و زبان فراگیر.
> - **Review your docs as code** فرآیند بازبینی مبتنی بر best practiceهای code review.
> - **Versions and releases: publish docs as code** مدیریت نسخه‌ها، انتشارها و استقرار مستندات هماهنگ با چرخهٔ توسعه.

> **What's new in the Second Edition?** Updated coverage of modern static site generators, expanded CI/CD automation examples, new case studies from teams at Sysdig, platformOS, and Redis, plus a deeper look at REST API documentation and OpenAPI workflows.

**در ویرایش دوم چه جدید است؟** پوشش به‌روزشدهٔ مولدهای سایت استاتیک مدرن، مثال‌های گسترده‌تر اتوماسیون CI/CD، مطالعات موردی جدید از تیم‌های Sysdig، platformOS و Redis، و نگاهی عمیق‌تر به مستندات REST API و گردش‌کارهای OpenAPI.

---

## درس‌ها و تمرین‌های رایگان

> 📚 Lessons & exercises → /learn/

مسیر آموزشی رایگان سایت شامل این موارد است:

```
learn/
├── 00-github-for-docs-files/       # GitHub for documentation sites
├── 000-docs-as-code-quick-start-guide/
├── 01-sphinx-python-rtd/          # Set Up Sphinx with Python
├── 02-jekyll-ruby-gh-pages/       # Set Up Jekyll with Ruby
├── 03-hugo-go-netlify/            # Set Up Hugo with Go
└── 04-add-content-workflow/       # Working with content in GitHub repositories
```

> Sphinx works with either major versions of Python active today... Sphinx is a documentation tool that creates HTML, CSS, and JavaScript files from ReStructured text files.
> Jekyll is a Static Site Generator that typically accepts Markdown for authoring.
> To build Hugo sites locally, install Homebrew and Hugo. You do not need to install Go to use Hugo as your static site generator.

- **Sphinx** ابزاری برای تولید HTML، CSS و JavaScript از فایل‌های ReStructuredText است (اکوسیستم پایتون، محبوب در مستندات Read the Docs).
- **Jekyll** یک مولد سایت استاتیک است که معمولاً Markdown می‌گیرد (اکوسیستم روبی، به‌شدت محبوب در GitHub Pages).
- **Hugo** یک مولد سایت استاتیک است (اکوسیستم Go). نکتهٔ جالب: برای استفاده از Hugo **لازم نیست** Go را نصب کنید.

> **نکتهٔ عملی:** انتخاب مولد سایت، تصمیمِ *محتوا* نیست؛ تصمیمِ *زیرساخت* است. مهم‌تر اینکه هر سه روی **Markdown + Git** کار می‌کنند، پس مهاجرت بین آن‌ها آسان است. این همان اصل «ابزار مهم‌تر از فرآیند نیست» است.

---

## چرا CODEOWNERS

> ### Protecting a Branch so Only the Docs Team Merges and Publishes
> When you want to allow the docs team members to maintain docs within a code repo, while giving the docs team autonomy over their own reviews and merges, you can use a protected branch and a CODEOWNERS file.

اگر می‌خواهید اعضای تیم مستندات بتوانند مستندات را داخل مخزن کد نگهداری کنند، اما در عین حال به تیم مستندات **اختیار مستقل** روی بازبینی و merge بدهید، می‌توانید از یک شاخهٔ محافظت‌شده به‌همراه فایل `CODEOWNERS` استفاده کنید.

> این یک راه‌حل **الگوریتمی ساده** برای یک مسئلهٔ سازمانی واقعی است: مستندات در مخزن کد (کنار کد) باشد، اما مالکیت کنترل آن دست تیم مستندات بماند.

---

## یادداشت شخصی

> **اهمیت این منبع:** Docs Like Code کمتر کتابی است که یک **تغییر پارادایم** را نام‌گذاری و ترویج کرده باشد. جملهٔ «بیایید مستندات را مثل کد مدیریت کنیم» از یک استعاره شروع شد و به یک صنعت تبدیل شد. اما ارزش واقعی‌اش نه در جمله، بلکه در **جزئیات اجرایی** است.
>
> **۱) مهم‌ترین چیزی که از این منبع برداشتم: صفر کردن فاصله.** بخش «کمتر از ۱۰ دقیقه» در ابتدای صفحه، ساده به‌نظر می‌رسد، اما در واقع کل فلسفهٔ کتاب در همان چند خط خلاصه شده: بنویس → commit کن → خودکار منتشر شد. وقتی فاصلهٔ «ویرایش تا انتشار» صفر باشد، دیگر هیچ بهانه‌ای برای عقب‌افتادن مستندات باقی نمی‌ماند. هر راه‌حل دیگری (Wiki، Word، Google Docs) این فاصله را مصنوعی نگه می‌دارد و همین، ریشهٔ مشکل است.
>
> **۲) مفهوم CODEOWNERS، راه‌حل یک مسئلهٔ واقعی سازمانی بود.** در محیط کاری ما، مستندات تیم دیگری بود و همین، ابزار را معطل کرده بود. راه‌حل‌های واقعی سازمانی همیشه یک لایهٔ انسانی دارند. اینکه کتاب این را پوشش می‌دهد، نشان می‌دهد فقط یک بحث نظری نیست.
>
> **۳) مطالعهٔ موردی Sysdig، ارزشمندترین بخش منابع این مجموعه بود.** این مقاله نشان می‌دهد docs-as-code چطور از یک **هاکاتون** شروع شد و چطور مرحله‌به‌مرحله به تولید رسید. این دقیقاً همان چیزی است که کتاب‌های نظری نمی‌گویند: مسیر واقعی، پر از ددلاک و بازگشت است.
>
> **۴) نقد و نکتهٔ من:** فصل «Test the docs» (lint، زبان فراگیر، DocOps) در بسیاری از پیاده‌سازی‌ها **نادیده گرفته می‌شود**، چون «زیبایی‌شناختی» به نظر می‌رسد. اما این دقیاً همان چیزی است که [*Living Documentation*](https://books.google.com/books/about/Living_Documentation.html?id=8_6ZDwAAQBAJ) به آن تکیه می‌کند: تستِ مستندات = تستِ کد. اگر docs-as-code را بدون lint و تستِ خودکار اجرا کنید، فقط یک سیستم فایلِ Markdown با تاریخچهٔ Git ساخته‌اید، نه «مستنداتِ زنده».
>
> **۵) جایگاهش در این مجموعه:** Docs Like Code **فرآیند** را پاسخ می‌دهد. Diátaxis **ساختار** را می‌دهد، Living Documentation **خودکارسازی** را. اگر این سه را کنار هم بگذارید، یک دستور کار کامل دارید. توصیهٔ من: ابتدا [*Diátaxis*](https://diataxis.fr/) را بخوانید (تا بدانید *چه* باید بنویسید)، بعد این را (تا بدانید *چگونه* نگهش دارید).

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۹/۳۰
**منبع اصلی:** [Docs Like Code - Anne Gentle](https://www.docslikecode.com/)
