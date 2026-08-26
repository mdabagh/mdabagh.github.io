## ۲۳. طراحی بر اساس قرارداد (Design by Contract)



![Pragmatic Paranoia](images/page001-145.png)

![Pragmatic Paranoia](images/page003-147.png)

![Pragmatic Paranoia](images/page005-149.png)

![Pragmatic Paranoia](images/page007-151.png)

![Pragmatic Paranoia](images/page009-153.png)

![Pragmatic Paranoia](images/page011-155.png)

![Pragmatic Paranoia](images/page013-157.png)

![Pragmatic Paranoia](images/page015-159.png)

![Pragmatic Paranoia](images/page017-161.png)

![Pragmatic Paranoia](images/page019-163-img1.png)

![Pragmatic Paranoia](images/page021-165.png)

![Pragmatic Paranoia](images/page023-167.png)

![Pragmatic Paranoia](images/page025-169.png)

---


> You Can't Write Perfect Software (Tip 36): Did that hurt? It shouldn't. Accept it as an axiom of life. Embrace it. Celebrate it. Because perfect software doesn't exist.
> Pragmatic Programmers build in defenses against their own mistakes.
> Design by Contract: Clients and suppliers must agree on rights and responsibilities.
> In Programming by Contract, we define the exact conditions under which a routine works: its preconditions, postconditions, and invariants.

نمی‌توانید نرم‌افزار کامل بنویسید (نکته ۳۶): درد داشت؟ نباید داشته باشد. آن را به عنوان یک اصل زندگی بپذیرید. آغوش بگیرید. جشن بگیرید. چون نرم‌افزار کامل وجود ندارد.
برنامه‌نویسان عملگرا دفاع‌هایی در برابر اشتباهات خودشان ایجاد می‌کنند.
طراحی بر اساس قرارداد: مشتریان و تأمین‌کنندگان باید در مورد حقوق و مسئولیت‌ها توافق کنند.

---

## ۲۴. برنامه‌های مرده دروغ نمی‌گویند (Dead Programs Tell No Lies)

> All errors give you information. You could convince yourself that the error can't happen, and choose to ignore it. Instead, Pragmatic Programmers tell themselves that if there is an error, something very, very bad has happened.
> Crash Early (Tip 38): A dead program normally does a lot less damage than a crippled one.
> Crash, Don't Trash: One of the benefits of detecting problems as soon as you can is that you can crash earlier, and crashing is often the best thing you can do.
> Erlang and Elixir embrace this philosophy. Joe Armstrong is often quoted as saying, "Defensive programming is a waste of time. Let it crash!"

تمام خطاها به شما اطلاعات می‌دهند. می‌توانید به خودتان بقبولانید که خطا نمی‌تواند اتفاق بیفتد و آن را نادیده بگیرید. در عوض، برنامه‌نویسان عملگرا به خود می‌گویند اگر خطایی وجود دارد، چیز بسیار بدی اتفاق افتاده است.
زود خراب شوید (نکته ۳۸): یک برنامه مرده معمولاً آسیب بسیار کمتری نسبت به یک برنامه فلج‌شده ایجاد می‌کند.
خراب شوید، خراب نکنید: یکی از مزایای تشخیص مشکلات در اسرع وقت این است که می‌توانید زودتر خراب شوید.
زبان‌های Erlang و Elixir این فلسفه را در آغوش می‌گیرند. جو آرم‌استرانگ اغلب نقل قول می‌شود: "برنامه‌نویسی دفاعی هدر دادن وقت است. بگذارید خراب شود!"

---

## ۲۵. برنامه‌نویسی مبتنی بر assertion (Assertive Programming)

> Use Assertions to Prevent the Impossible (Tip 39): Whenever you find yourself thinking "but of course that could never happen," add code to check it.
> Don't use assertions in place of real error handling. Assertions check for things that should never happen.
> Leave Assertions Turned On: There is a common misunderstanding about assertions. Assertions add some overhead to code, but the benefits outweigh the costs.

از assertion برای جلوگیری از غیرممکن استفاده کنید (نکته ۳۹): هر زمان که به خود فکر می‌کنید "البته این هرگز نمی‌تواند اتفاق بیفتد"، کدی برای بررسی آن اضافه کنید.
از assertion به جای مدیریت خطای واقعی استفاده نکنید.
Assertion را روشن نگه دارید: سوءتفاهم رایجی درباره assertion وجود دارد.

---

## ۲۶. چگونه منابع را متعادل کنیم (How to Balance Resources)

> Don't Outrun Your Headlights (Tip 40): We stick to small steps always, so we don't fall off the edge of the cliff.
> When you allocate a resource, make sure that you, and only you, are responsible for deallocating it. This applies to memory, files, devices, network connections, database locks, and any other finite resource.
> Always allocate as late as possible, and free as early as possible.

از چراغ‌های جلو پیشی نگیرید (نکته ۴۰): همیشه به قدم‌های کوچک پایبند باشید تا از لبه پرتگاه نیفتید.
وقتی منبعی تخصیص می‌دهید، مطمئن شوید شما و فقط شما مسئول آزادسازی آن هستید.
همیشه دیرتر تخصیص دهید و زودتر آزاد کنید.

---

## ۲۷. از چراغ‌های جلو پیشی نگیرید (Don't Outrun Your Headlights)

> The only way to make big gains in a complex system is to break the work into small, manageable chunks.
> Don't outrun your headlights: make sure you can stop where you think you are. Take small, measured steps. Prototype to learn.

تنها راه برای کسب درآمدهای بزرگ در یک سیستم پیچیده این است که کار را به قطعات کوچک و قابل مدیریت تقسیم کنید.
از چراغ‌های جلو پیشی نگیرید: مطمئن شوید می‌توانید جایی که فکر می‌کنید هستید متوقف شوید. قدم‌های کوچک و اندازه‌گیری شده بردارید.

---

# فصل پنجم: انعطاف یا شکست ⏱️ ۲۰ دقیقه مطالعه