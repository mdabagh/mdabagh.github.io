> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی کتاب/معرفی به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: مستندات زنده — Living Documentation

> **منبع اصلی:** Living Documentation — Using Documentation as a Product to Enhance Software Quality
> **نویسنده:** Cyrille Martraire
> **انتشار:** Addison-Wesley Professional (نسخهٔ چاپی و الکترونیکی) / نسخهٔ اصلی در Leanpub
> **لینک:** https://books.google.com/books/about/Living_Documentation.html?id=8_6ZDwAAQBAJ
> **نسخهٔ Leanpub:** https://leanpub.com/livingdocumentation
> **نوع:** کتاب (نسخهٔ Leanpub: ۴۷۸ صفحه / ۱۲۵٬۵۵۶ کلمه — کامل‌شده در ۱۴۰۸/۰۳/۲۴)

---

## چکیده

> You don't necessarily have to choose between Working Software and Extensive Documentation! Discover how a Living Documentation can help you in all aspects of your projects, from the business goals to the business domain knowledge, architecture and design, processes and deployment, even if you hate writing documentation.

**لازم نیست** میان «نرم‌افزارِ کارآمد» و «مستنداتِ گسترده» یکی را انتخاب کنید!
دریابید چگونه یک **مستندِ زنده** (Living Documentation) می‌تواند در همهٔ جنبه‌های پروژه‌های شما — از اهداف کسب‌وکار تا دانش دامنهٔ کسب‌وکار، معماری و طراحی، فرآیندها و استقرار — کمک کند، حتی اگر از نوشتن مستندات بیزارید.

> The approach "Specification by Example" has introduced the idea of a "Living Documentation". In this approach, examples of behavior are used for documentation and are also promoted into automated tests. Whenever a test fails, it signals the documentation is no longer in sync with the code so it can just be fixed quickly.
> This has shown that it is possible to have useful documentation that doesn't suffer the fate of getting obsolete once written.

رویکرد «**Specification by Example**» ایدهٔ «**مستندِ زنده**» را معرفی کرده است. در این رویکرد، **مثال‌هایی از رفتار** هم به‌عنوان مستندسازی استفاده می‌شوند و هم به **تست‌های خودکار** ارتقا می‌یابند. هر بار که یک تست شکست بخورد، این **نشان می‌دهد** که مستندات دیگر با کد هم‌گام نیست، بنابراین به‌سرعت قابل اصلاح است.

این نشان داده است که داشتن مستندات مفیدی که پس از نوشتن منسوخ نشوند، **امکان‌پذیر** است.

> But we can go much further. This book expands on this idea of a Living Documentation. It shows how a living documentation evolves at the same pace than the code, for all aspects of a project, from the business goals to the business domain knowledge, architecture and design, processes and deployment.

اما ما می‌توانیم بسیار فراتر برویم. این کتاب این ایدهٔ مستندِ زنده را بسط می‌دهد. نشان می‌دهد چگونه یک مستندِ زنده **با همان سرعت کد** و برای **همهٔ جنبه‌های** یک پروژه تکامل می‌یابد — از اهداف کسب‌وکار تا دانش دامنه، معماری و طراحی، فرآیندها و استقرار.

> This book explains the theory and describes a number of techniques, with illustrations and concrete examples. You will learn how to start investing into documentation that is always up to date, at a minimal extra cost thanks to well-crafted artifacts and the use of automation.

این کتاب نظریه را توضیح می‌دهد و تعدادی تکنیک را همراه با تصویر و مثال‌های عینی شرح می‌دهد. خواهید آموخت چگونه سرمایه‌گذاری بر مستنداتی را آغاز کنید که **همیشه** به‌روز است — با حداقل هزینهٔ اضافی، به‌لطف آرتیفکت‌های خوب‌ساخته و استفاده از اتوماسیون.

---

## مسئله: دوگانگی کاذب

> You don't necessarily have to choose between Working Software and Extensive Documentation!

این جمله، تمام هستهٔ فلسفهٔ کتاب است. صنعت نرم‌افزار سال‌ها درگیر یک **دوگانگی کاذب** بوده است:

| قطب اول | قطب دوم | تصور رایج |
|---|---|---|
| نرم‌افزارِ کارآمد | مستنداتِ گسترده | «انتخاب کن: یا کد یا مستند» |
| زمان رسیدن به بازار | کیفیت دانش | «نوشتن مستندات = کند شدن» |
| نگهداری ویژگی | نگهداری دانش | «مستندات یعنی کار اضافه» |

> **نکتهٔ کلیدی کتاب:** این دوگانگی **واقعی نیست**. مسئله در این بوده که «مستندات» را با یک شکل خاص (سند ایستا، جدا از کد، نوشته‌شده در انتهای پروژه) اشتباه گرفته بودیم. اگر شکل را عوض کنیم، دوگانگی از بین می‌رود.

> **به زبان ساده:** مسئله این نیست که «مستندات بنویسیم یا نه». مسئله این است که «مستندات را **چه شکلی** تولید کنیم». شکلِ سندِ ایستا گران است؛ شکلِ مستندِ زنده تقریباً رایگان است. تمام کتاب دربارهٔ تغییر شکل است.

---

## ریشه: Specification by Example

> The approach "Specification by Example" has introduced the idea of a "Living Documentation". In this approach, examples of behavior are used for documentation and are also promoted into automated tests. Whenever a test fails, it signals the documentation is no longer in sync with the code so it can just be fixed quickly.

ریشهٔ ایده در رویکرد **«مشخصات به‌وسیلهٔ مثال» (Specification by Example / BDD)** است:

```
مثال رفتاری  ──►  مستندات      (برای انسان‌ها)
      │
      └────────►  تست خودکار   (برای ماشین‌ها)

                (یک منبع واحد برای هر دو)

اگر تست FAIL شود ──►  مستند دیگر هم‌گام نیست ──►  باید اصلاح شود
```

**نکتهٔ انفجاری این سازوکار:** همان یک مثال، هم‌زمان دو کار می‌کند. یعنی هزینهٔ تولید مستندات، عملاً **صفر** می‌شود، چون قبلاً برای نوشتن تست هزینه می‌کردید و حالا همان هزینه، دو خروجی تولید می‌کند.

> **به زبان ساده:** «آزمون» و «مستند» دو چیز جدا نیستند. هر تست خودکار، در واقع یک پاراگراف مستندات هم هست. هر پاراگراف مستندات، اگر قابل‌اجرا باشد، یک تست هم هست. کتاب می‌گوید: این دو را در **یک آرتیفکت** ادغام کن.

---

## توسعهٔ ایده: مستندات زنده برای همهٔ جنبه‌ها

> It shows how a living documentation evolves at the same pace than the code, for all aspects of a project, from the business goals to the business domain knowledge, architecture and design, processes and deployment.

کتاب ایدهٔ اولیهٔ Specification by Example را به **کل چرخهٔ عمر** گسترش می‌دهد. نکتهٔ مهم این است که «مستند زنده» فقط برای **رفتار کد** نیست:

| جنبهٔ پروژه | آرتیفکت زندهٔ متناظر |
|---|---|
| **اهداف کسب‌وکار** | بیانیهٔ مسئله / فرضیات کشف‌شده — به‌روزشده با بازخورد بازار |
| **دانش دامنه** | مدل زبان مشترک (Ubiquitous Language) — استخراج‌شده از کد و مکالمه |
| **معماری و طراحی** | تصمیم‌های معماری (ADR) — ثبت در لحظهٔ تصمیم، نه بعداً |
| **فرآیندها** | فرآیندهای قابل‌اجرا / خط لولهٔ CI |
| **استقرار** | پیکربندی به‌عنوان کد — همان‌طور که مستندات، کد است |

> **نکتهٔ ظریف:** «همان سرعت کد» یعنی **دقیقاً هم‌سرعت**. نه سریع‌تر، نه کندتر. اگر مستندات سریع‌تر از کد به‌روز شوند، یعنی دارید چیزی می‌نویسید که هنوز واقعیت ندارد.

---

## زبان مشترک: نقطهٔ اتصال مستندات و کد

این یکی از مفاهیم کلیدی کتاب است و از ادبیات Domain-Driven Design می‌آید:

> از آنجا که بسیاری از واژگانِ «دانش دامنه» فقط در ذهنِ افراد زندگی می‌کنند و در کد منعکس نمی‌شوند، **نام‌گذاری** مهم‌ترین شکلِ ذخیرهٔ دانش است. اگر نام متد `calculateOrderTotal` است، معنای «محاسبهٔ مجموع سفارش» بدون هیچ سندی منتقل می‌شود.

> **به زبان ساده:** نام‌ها را جدی بگیرید. `handle2()` هیچ چیزی منتقل نمی‌کند. `applyLoyaltyDiscount(order, customer)` هم **مستند** است و هم **کد** است. این ارزان‌ترین نوع مستندسازی ممکن است.

---

## اصل «حداقل هزینهٔ اضافی»

> You will learn how to start investing into documentation that is always up to date, at a minimal extra cost thanks to well-crafted artifacts and the use of automation.

معیار موفقیت یک روش مستندسازی، **کیفیت مستندات نیست؛ هزینهٔ آن است**. کتاب معیار را عوض می‌کند:

> اگر ساختن مستنداتِ زنده، ۱۰٪ زمان اضافه بگیرد، مردم نمی‌سازندش. اگر ۱٪ باشد، شاید. اگر **صفر** باشد (چون هزینه از قبل برای چیز دیگری پرداخت می‌شد)، قطعاً انجام می‌شود.

> **به زبان ساده:** بهترین مستندسازی آن است که هزینهٔ **حاشیه‌ای** آن صفر باشد. این دقیقاً همان چیزی است که در مقالهٔ [Lethbridge et al. 2003](https://ieeexplore.ieee.org/document/1241364) به‌عنوان محدودیت اصلی شناسایی شد: «مهندسان محدودیت زمانی دارند». پاسخ مستندات زنده به همان محدودیت است.

---

## دربارهٔ نویسنده

> Cyrille Martraire is a passionate developer since 1999. He's the co-founder and CTO of Arolla, a company specializing in software development and nothing else. With a love-and-hate relationship with documentation, ...

سیریل ماترِر (Cyrille Martraire) از سال ۱۹۹۹ توسعه‌دهنده است. او هم‌بنیان‌گذار و CTO شرکت Arolla است که تنها در زمینهٔ توسعهٔ نرم‌افزار تخصص دارد. جملهٔ کلیدی بیوگرافی‌اش: «با رابطه‌ای از عشق و نفرت با مستندات...».

> **نکتهٔ تأملی:** کسی که رابطه‌اش با مستندات «عشق و نفرت» است، دقیقاً کسی است که بهترین نوشته‌ها را در این حوزه دارد. چون از درونِ رنج نوشته، نه از بیرون. این با الگوی مشترک در ادبیات مستندسازی هم‌خوان است: بهترین کتاب‌های این حوزه را کسانی نوشته‌اند که دردِ آن را کشیده‌اند.

---

## یادداشت شخصی

> **اهمیت این کتاب:** اگر [*Docs Like Code*](https://www.docslikecode.com/) بگوید «مستندات را مثل **کد** مدیریت کن»، این کتاب یک قدم جلوتر می‌رود و می‌گوید: «مستندات باید مثل **تست** زنده بمانند». این تفاوت ظریفی است که کل ایدهٔ کتاب را می‌سازد.
>
> **۱) مهم‌ترین ایدهٔ کتاب در یک جمله: «کیفیت مستندات را با هزینه‌اش بسنج، نه با زیبایی‌اش».** جملهٔ «at a minimal extra cost» کلید فهم کتاب است. این کتاب دربارهٔ **زیبایی** نیست؛ دربارهٔ **اقتصاد** است. و اقتصاد، چیزی است که سازمان‌ها را حرکت می‌دهد.
>
> **۲) چیزی که برایم تکان‌دهنده بود: گسترش از کد به کسب‌وکار.** اکثر ابزارهای مستندسازی (حتی پیشرفته‌ترین‌شان) فقط **کد** را پوشش می‌دهند. اما کتاب می‌گوید مستنداتِ زندهٔ واقعی از **اهداف کسب‌وکار** شروع می‌شود. این نگاه، سطح بحث را عوض می‌کند: مستندسازی دیگر یک وظیفهٔ فنی نیست، یک **سازوکار یادگیری سازمانی** است.
>
> **۳) هشدار صادقانه:** عناوین و توضیحات عمومی این کتاب در دسترس است، اما متن کامل آن (حتی نسخهٔ Leanpub) پشت پرداخت است. ترجمهٔ این پست بر پایهٔ معرفی رسمی نویسنده و صفحهٔ ناشر روی Leanpub و Addison-Wesley است، نه متن فصل‌ها. ساختار و منطق کتاب از همین منابع روشن است، ولی برای استفادهٔ کامل باید کتاب تهیه شود.
>
> **۴) مهم‌ترین انتقاد من:** ایدهٔ «مستندات زنده» گران تمام می‌شود اگر بخواهید آن را به حوزه‌هایی ببرید که ذاتاً **غیرقابل‌تست‌شدن** هستند — مثل «ارزش‌های فرهنگی» یا «نیازهای آیندهٔ کسب‌وکار». جادوی مستندات زنده وقتی کار می‌کند که چیزی **قابل‌اجرا** باشد. این محدودیت را کتاب صریح نمی‌گوید، اما عملاً از دلش فهمیده می‌شود.
>
> **۵) جایگاهش در این مجموعه و پیوندهایش:** ترکیب این چهار منبع، یک معماری کامل می‌سازد:
> - [*Diátaxis*](https://diataxis.fr/) می‌گوید **چه** بنویسید (طبقه‌بندی چهارگانه)
> - [*Docs for Developers*](https://link.springer.com/book/10.1007/979-8-8688-2509-5) می‌گوید **چگونه** بنویسید (فصل ۶: نمونه‌های کد)
> - [*Docs Like Code*](https://www.docslikecode.com/) می‌گوید **چگونه** نگهش دارید (Git، CI، PR)
> - **Living Documentation** می‌گوید **چگونه** اصلاً فراموششان نکنید (تست = مستند)
>
> جمله‌ای که از این ترکیب برداشتم: **نویسندهٔ خوب، موفق‌ترین کاری را می‌کند که می‌تواند بکند — نمی‌نویسد.**
>
> **پیشنهاد من:** اگر تیم شما الان دارد مستندات دستی می‌نویسد، این کتاب را بخوانید و فقط **یک** بخش را اجرا کنید: تست‌های قابل‌اجرا به‌عنوان مستندات. اگر جواب داد، بقیه‌اش را ادامه دهید. اگر نداد، حداقل چیزی برای بهینه‌سازی دارید.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۹/۳۰
**منبع اصلی:** [Google Books - Living Documentation - Cyrille Martraire](https://books.google.com/books/about/Living_Documentation.html?id=8_6ZDwAAQBAJ)
