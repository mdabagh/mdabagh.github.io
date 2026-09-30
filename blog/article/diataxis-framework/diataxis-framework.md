> **راهنمای مطالعه**
>
> در هر بخش، ابتدا متن اصلی به زبان انگلیسی آورده شده و سپس ترجمه و توضیحات فارسی همان بخش ارائه شده است.

---
# ترجمه فارسی: Diátaxis — چارچوب نظام‌مند مستندسازی

> **منبع اصلی:** Diátaxis — A systematic approach to technical documentation authoring
> **نویسنده:** Daniele Procida
> **لینک:** https://diataxis.fr/
> **نوع:** چارچوب نظری-عملی (وب‌سایت رایگان، دارای ترجمه به چندین زبان)

---

## چکیده

> Diátaxis is a way of thinking about and doing documentation.
> It prescribes approaches to content, architecture and form that emerge from a systematic approach to understanding the needs of documentation users.
> Diátaxis identifies four distinct needs, and four corresponding forms of documentation - *tutorials*, *how-to guides*, *technical reference* and *explanation*. It places them in a systematic relationship, and proposes that documentation should itself be organised around the structures of those needs.

**Diátaxis** روشی برای **فکر کردن** و **انجام دادن** مستندسازی است.

این چارچوب، رویکردهایی برای **محتوا**، **معماری** و **فرم** ارائه می‌دهد که از یک رویکرد نظام‌مند به فهم **نیازهای کاربران مستندات** پدید آمده‌اند.

Diátaxis چهار نیاز متمایز و چهار شکل متناظر مستندات را شناسایی می‌کند — *آموزش‌ها* (tutorials)، *راهنماهای گام‌به‌گام* (how-to guides)، *مرجع فنی* (technical reference) و *توضیح/تبیین* (explanation). این‌ها را در یک رابطهٔ نظام‌مند قرار می‌دهد و پیشنهاد می‌کند که مستندات خود نیز حول ساختار همین نیازها سازمان یابند.

> *Diátaxis*, from the Ancient Greek δῐᾰ́τᾰξῐς: *dia* ("across") and *taxis* ("arrangement").

واژهٔ *Diátaxis* از یونانی باستان **δῐᾰ́τᾰξῐς** آمده است: *dia* به‌معنای «در سراسر / فراتر» و *taxis* به‌معنای «چیدمان / ترتیب».

> Diátaxis solves problems related to documentation *content* (what to write), *style* (how to write it) and *architecture* (how to organise it).

Diátaxis مسائل مربوط به **محتوا** (چه چیزی بنویسیم)، **سبک** (چگونه بنویسیم) و **معماری** (چگونه سازمان دهیم) مستندات را حل می‌کند.

> As well as serving the users of documentation, Diátaxis has value for documentation creators and maintainers. It is light-weight, easy to grasp and straightforward to apply. It doesn't impose implementation constraints. It brings an active principle of quality to documentation that helps maintainers think effectively about their own work.

علاوه بر خدمت به **کاربران** مستندات، Diátaxis برای **آفرینندگان و نگهدارندگان** مستندات هم ارزشمند است. سبک‌وزن است، به‌سادگی درک می‌شود و به‌روشنی قابل‌اعمال است. هیچ قیدی بر پیاده‌سازی تحمیل نمی‌کند و یک **اصل فعال کیفیت** را به مستندات می‌آورد که به نگهدارندگان کمک می‌کند مؤثرتر فکر کنند.

---

## بُعد اول: شناخت کاربر

> Diátaxis is based on the principle that documentation must serve the needs of its users. Knowing how to do that means understanding what the needs of users are.

Diátaxis بر این اصل بنا شده که **مستندات باید در خدمت نیازهای کاربرانش باشد**. برای دانستن چگونه این کار را کرد، باید نیازهای کاربران را بفهمیم.

> The user whose needs Diátaxis serves is *the practitioner in a domain of skill*. A domain of skill is defined by a craft - the use of a tool or product is a craft. So is an entire discipline or profession. Using a programming language is a craft, as is flying a particular aircraft, or even being a pilot in general.

کاربری که Diátaxis به نیازهای او خدمت می‌کند، **یک تمرین‌کرده در یک حوزهٔ مهارت** است. یک حوزهٔ مهارت با یک **صنعت‌دستی (craft)** تعریف می‌شود — استفاده از یک ابزار یا محصول، یک صنعت است. کل یک رشته یا حرفه هم همین‌طور. استفاده از یک زبان برنامه‌نویسی یک صنعت است، همان‌طور که پرواز با یک هواپیمای مشخص، یا حتی خلبان بودن به‌طور کلی.

> Understanding the needs of these users means in turn understanding the essential characteristics of craft or skill.

درک نیازهای این کاربران یعنی درک ویژگی‌های بنیادی صنعت یا مهارت.

---

## بُعد دوم: اکتساب در برابر کاربرد

> Similarly, the relationship of a practitioner with their practice is that it is something that needs to be both *acquired*, and *applied*. Being "at work" (concerned with applying the skill and knowledge of their craft) and being "at study" (concerned with acquiring them) are once again counterparts, distinct but bound up with each other.

به‌طور مشابه، رابطهٔ یک تمرین‌کرده با حرفهٔ او این است که آن چیزی است که باید هم **اکتساب** شود و هم **به‌کار** رود. «سرِ کار» بودن (نگرانِ به‌کارگیری مهارت و دانش) و «در حال مطالعه» بودن (نگرانِ اکتساب آن‌ها)، دوباره **مقابل‌هایی** هستند: متمایز، اما عمیقاً به هم گره‌خورده.

> A skill or craft or practice contains both *action* (practical knowledge, knowing *how*, what we do) and *cognition* (theoretical knowledge, knowing *that*, what we think). The two are completely bound up with each other, but they are counterparts, wholly distinct from each other, two different aspects of the same thing.

هر مهارت یا صنعت، هم **کنش** (دانش عملی، دانستنِ *چگونه*، آنچه انجام می‌دهیم) و هم **شناخت** (دانش نظری، دانستنِ *اینکه*، آنچه می‌اندیشیم) را در بر می‌گیرد. این دو کاملاً به هم گره خورده‌اند، اما **مقابل** یکدیگرند — کاملاً متمایز، دو جنبهٔ متفاوت از یک چیز واحد.

---

## نقشهٔ سرزمین

> This gives us two dimensions of skill, that we can lay out on a map - a map of the territory of craft:
> This is a *complete* map. There are only two dimensions, and they don't just cover the entire territory, they define it. This is why there are necessarily four quarters to it, and there could not be three, or five. It is not an arbitrary number.

این به ما **دو بُعد** از مهارت می‌دهد که می‌توانیم روی نقشه‌ای بگذاریم — نقشهٔ سرزمینِ صنعت:

```
                    ACQUISITION                     APPLICATION
                (اکتساب: یادگیری)              (کاربرد: به‌کارگیری)
              ┌───────────────────────┬───────────────────────┐
   ACTION     │                       │                       │
  (کنش:      │      TUTORIALS        │     HOW-TO GUIDES     │
   انجام دادن)│      آموزش گام‌به‌گام │      راهنمای عملی     │
              │                       │                       │
              ├───────────────────────┼───────────────────────┤
 COGNITION    │                       │                       │
 (شناخت:     │      EXPLANATION       │      REFERENCE        │
  اندیشیدن)  │      تبیین و توضیح    │      مرجع فنی         │
              │                       │                       │
              └───────────────────────┴───────────────────────┘
```

> **این نقشه کامل است.** فقط دو بُعد وجود دارد، و این دو بُعد فقط قلمرو را پوشش نمی‌دهند، بلکه **تعریفش** می‌کنند. به همین دلیل است که الزاماً **چهار** ربع وجود دارد، و نه سه یا پنج. این یک عدد دلخواه نیست.

> **به زبان ساده:** چهار نوع مستند، یک سلیقهٔ زیبایی‌شناختی نیست. از دلِ دو بُعدِ بنیادیِ «یادگیری/کار» و «انجام/فهمیدن» **به‌صورت منطقی** بیرون می‌آید. اگر کسی بگوید «ما پنج نوع مستند داریم»، یعنی جایی از نقشه اشتباه کرده — یا یکی از چهار ربع را دو شکسته یا دو تا را در یکی ادغام کرده است.

---

## جدول نیازها

> need: learning | how-to | information | understanding
> addressed in: informs action | informs action | informs cognition | informs cognition

| نیاز | شکل مستندات | نوع چیزی که به آن می‌دهد |
|---|---|---|
| **یادگیری** (learning) | **Tutorials** | اقدام (action) را آموزش می‌دهد |
| **انجام کار** (goals) | **How-to guides** | اقدام (action) را آموزش می‌دهد |
| **اطلاعات** (information) | **Reference** | شناخت (cognition) را آموزش می‌دهد |
| **فهمیدن** (understanding) | **Explanation** | شناخت (cognition) را آموزش می‌دهد |

> **به زبان ساده:** نیمی از مستندات (تutorial و how-to) به شما **آینده** می‌دهند — چه کاری انجام دهید. نیم دیگر (reference و explanation) به شما **گذشته/کنون** می‌دهند — چه چیزی هست و چرا. اینکه کدام را می‌نویسید، کاملاً بستگی دارد به اینکه کاربرِ شما در آن لحظه در کدام قطب ایستاده.

---

## قطب‌نما: ابزار تصمیم‌گیری

> The Diátaxis compass is something like a truth-table or decision-tree of documentation. It reduces a more complex, two-dimensional problem to its simpler parts, and provides the author with a course-correction tool.

**قطب‌نمای Diátaxis** چیزی شبیه یک جدول حقیقت (truth-table) یا درخت تصمیم‌گیری برای مستندات است. مسئلهٔ پیچیده و دوبعدی را به بخش‌های ساده‌اش کاهش می‌دهد و ابزاری برای اصلاح مسیر به نویسنده می‌دهد.

> If the content… …and serves the user's… …then it must belong to…
> informs action + acquisition of skill → **a tutorial**
> informs action + application of skill → **a how-to guide**
> informs cognition + application of skill → **reference**
> informs cognition + acquisition of skill → **explanation**

اگر محتوا… **و** در خدمت نیاز کاربر باشد… **آنگاه** باید متعلق باشد به:

| محتوا | نیاز کاربر | نوع مستند |
|---|---|---|
| اقدام (action) | اکتساب مهارت | **Tutorial** |
| اقدام (action) | کاربرد مهارت | **How-to guide** |
| شناخت (cognition) | کاربرد مهارت | **Reference** |
| شناخت (cognition) | اکتساب مهارت | **Explanation** |

> To use the compass, just two questions need to be asked: *action or cognition? acquisition or application?* And it yields the answer.

برای استفاده از قطب‌نما فقط دو پرسش لازم است: **اقدام یا شناخت؟** **اکتساب یا کاربرد؟** و پاسخ به دست می‌آید.

> **Worse, sometimes intuition provides an immediate answer that is also wrong.**

بدتر اینکه، گاهی شهود، پاسخی فوری و **اشتباه** می‌دهد.

> A map is most powerful in unfamiliar territory when we also have a compass to guide us.

نقشه زمانی بیشترین قدرت را دارد که در سرزمین ناآشنا باشیم و قطب‌نمایی هم برای هدایت داشته باشیم.

---

## واژگان عملی قطب‌نما

> - action: practical steps, doing
> - cognition: theoretical or propositional knowledge, thinking
> - acquisition: study
> - application: work

- **action**: گام‌های عملی، انجام دادن
- **cognition**: دانش نظری یا گزاره‌ای، اندیشیدن
- **acquisition**: مطالعه
- **application**: کار

> And the questions themselves can also be used in different ways:
> - Do I think I am writing for *x* or *y*?
> - Is this writing in front of me engaged in *x* or *y*?
> - Does the user need *x* or *y*?
> - Do I want to *x* or *y*?

خودِ پرسش‌ها هم به شیوه‌های مختلفی قابل‌استفاده‌اند:
- آیا فکر می‌کنم برای **X** یا **Y** می‌نویسم؟
- آیا این نوشتهٔ روبه‌روی من مشغول **X** یا **Y** است؟
- آیا کاربر به **X** یا **Y** نیاز دارد؟
- آیا می‌خواهم **X** یا **Y** را انجام دهم؟

> And try applying them close-up, at the level of sentences and words, or from a wider perspective, considering an entire document.

و سعی کنید آن‌ها را از نزدیک، در سطح جمله و کلمه، یا از دید گسترده‌تر و با در نظر گرفتن کل سند، به کار ببرید.

---

## چرا Diátaxis کار می‌کند

> Diátaxis is successful because it *works* - both users and creators have a better experience of documentation as a result. It makes sense and it feels right.
> However, that’s not enough to be confident in Diátaxis as a theory of documentation. As a theory, it needs to show *why* it works. It needs to show that there is actually some reason why there are exactly four kinds of documentation, not three or five. It needs to demonstrate rigorous thinking and analysis, and that it stands on a sound theoretical foundation.
> Otherwise, it will be just another useful heuristic approach, and the strongest claim we can make for it is that "it seems to work quite well".

Diátaxis موفق است چون **کار می‌کند** — هم کاربران و هم آفرینندگان تجربهٔ بهتری از مستندات دارند. منطقی است و درست به‌نظر می‌رسد.

اما این برای اطمینان از آن به‌عنوان یک **نظریه** کافی نیست. به‌عنوان نظریه، باید نشان دهد **چرا** کار می‌کند. باید نشان دهد دلیلی وجود دارد که چرا دقیقاً **چهار** نوع مستندات وجود دارد، نه سه یا پنج. باید تفکر و تحلیل دقیق را نشان دهد و اینکه بر پایهٔ بنیانی نظری استوار ایستاده. در غیر این صورت، تنها یک رویکردheuristic مفید دیگر است و قوی‌ترین ادعایی که می‌توانیم دربارهٔ آن داشته باشیم این است که «به‌نظر می‌رسد خوب کار کند».

---

## بازخورد صنعتی

> Diátaxis has allowed us to build a high-quality set of internal documentation that our users love, and our contributors love adding to. — Greg Frileux, Vonage

> Diátaxis به ما اجازه داد مجموعه‌ای باکیفیت از مستندات داخلی بسازیم که کاربرانمان دوستش دارند و مشارکت‌کنندگانمان دوست دارند به آن اضافه کنند. — گرگ فریلو، Vonage

> At Gatsby we recently reorganized our open-source documentation, and the Diátaxis framework was our go-to resource throughout the project. The four quadrants helped us prioritize the user's goal for each type of documentation. By restructuring our documentation around the Diátaxis framework, we made it easier for users to discover the resources that they need when they need them. — Megan Sullivan, Gatsby

> در شرکت Gatsby اخیراً مستندات متن‌بازمان را بازسازماندهی کردیم و چارچوب Diátaxis منبع اصلی ما در طول پروژه بود. چهار ربع، به ما کمک کرد اولویت هدف کاربر را برای هر نوع مستند مشخص کنیم. — مگان سالیوان، Gatsby

> While redesigning the Cloudflare developer docs, Diátaxis became our north star for information architecture. When we weren't sure where a new piece of content should fit in, we'd consult the framework. Our documentation is now clearer than it's ever been, both for readers and contributors. — Adam Schwartz, Cloudflare

> هنگام بازطراحی مستندات توسعه‌دهندهٔ Cloudflare، Diátaxis قطب‌نمای ما برای معماری اطلاعات شد. هر وقت مطمئن نبودیم یک محتوای جدید کجا باید بنشیند، به چارچوب مراجعه می‌کردیم. مستندات ما اکنون روشن‌تر از هر زمان دیگری است. — آدام شوارتز، Cloudflare

---

## یادداشت شخصی

> **اهمیت این چارچوب:** Diátaxis نادرترین چیزی است که یک صنعت می‌تواند تولید کند: یک **نظریهٔ کامل** برای چیزی که تا آن زمان فقط «شهود» بود. پیش از Diátaxis، همه می‌دانستند مستندات خوب باید آموزش، مرجع و توضیح داشته باشد — اما هیچ‌کس نمی‌توانست بگوید **چرا دقیقاً این چهار**.
>
> **۱) مهم‌ترین نکته: این یک چارچوب «انتخابی» است، نه «فهرست کارها».** جملهٔ کلیدی صفحهٔ اصلی این است: «It solves problems related to content, style and architecture». یعنی وقتی نمی‌دانید چه بنویسید (محتوا)، چطور بنویسید (سبک) یا چطور چیدمانش کنید (معماری)، سراغ قطب‌نما بروید. این تفاوت بین «یک چک‌لیست» و «یک نظریه» است.
>
> **۲) چیزی که بلافاصله ذهنم را تکان داد: ستون «نه فقط برای کاربران».** تقریباً همهٔ کتاب‌های مستندسازی فقط از زاویهٔ کاربر حرف می‌زنند. Diátaxis صریحاً می‌گوید این چارچوب برای **نگهدارنده** هم ارزش دارد، چون به او یک اصل فعال کیفیت می‌دهد. این همان چیزی است که در [Google Style Guide](https://google.github.io/styleguide/docguide/best_practices.html) با عنوان «minimum viable documentation» مطرح می‌شود — و Diátaxis آن را **نظریه** می‌کند.
>
> **۳) جمله‌ای که در دفترم نوشتم:** «وقتی حس می‌کنم مستنداتم آشفته است، مشکل از نگارش نیست، از طبقه‌بندی است.» این تفکیک، خیلی از وقت‌هایی را که صرف «بازنویسی» می‌کردم، صرفه‌جویی کرد. مسئلهٔ چهار ربع، مسئلهٔ **انتخاب** است، نه **نوشتن**.
>
> **۴) نقد من: تقسیم‌بندی در عمل همیشه تمیز نیست.** نمودار چهار ربع بسیار زیباست، اما در پروژه‌های واقعی، محتوای واقعی همیشه داخل یک ربع تمیز جا نمی‌شود. به‌ویژه `how-to guide` و `tutorial` بیشترین هم‌پوشانی را دارند. با این حال، خودِ Procida این را می‌داند و به همین دلیل «قطب‌نما» را ساخته تا ابزار **اصلاح مسیر** باشد نه حکم نهایی. این صداقت، از ادعای مطلق بودن، ارزشمندتر است.
>
> **۵) جایگاهش در این مجموعه:** Diátaxis **ساختار** می‌دهد. اما یک هشدار مهم: Diátaxis به شما نمی‌گوید مستندات چطور **زنده** بمانند. اگر ساختار درست باشد ولی مستندات پس از ۶ ماه منسوخ شوند، شکست خورده‌اید. برای آن بخش باید سراغ [*Docs Like Code*](https://www.docslikecode.com/) و [*Living Documentation*](https://books.google.com/books/about/Living_Documentation.html?id=8_6ZDwAAQBAJ) بروید.
>
> **پیشنهاد من:** اگر فقط یک چیز از این مجموعه برمی‌دارید، Diátaxis باشد. چون بقیهٔ منابع بدون یک ساختار مشخص، به ابزارهای بی‌هدف تبدیل می‌شوند. صفحهٔ `Start here` سایت، بهترین نقطهٔ شروع است و در ۲۰ دقیقه خوانده می‌شود.

---

**ترجمه فارسی:** احمد مطلبی
**تاریخ ترجمه:** ۲۰۲۶/۰۹/۳۰
**منبع اصلی:** [Diátaxis - Daniele Procida](https://diataxis.fr/)
