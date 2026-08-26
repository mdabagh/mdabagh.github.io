# راهنمای مطالعه: برنامه‌نویس عملگرا (The Pragmatic Programmer)

> **عنوان اصلی:** The Pragmatic Programmer: Your Journey to Mastery  
> **نویسندگان:** David Thomas, Andrew Hunt  
> **ناشر:** Addison-Wesley  
> **سال انتشار:** ۲۰۱۹ (ویرایش بیستم)  
> **تعداد صفحات:** ۳۲۰

---

## چرا این کتاب را بخوانیم؟

> The Pragmatic Programmer is one of the most influential books on software development. Written in 1999 and updated for the 20th anniversary, it covers timeless principles that every programmer should know—from personal responsibility and career development to architectural techniques for keeping your code flexible and easy to change.

برنامه‌نویس عملگرا یکی از تأثیرگذارترین کتاب‌ها در حوزهٔ توسعهٔ نرم‌افزار است. این کتاب در سال ۱۹۹۹ نوشته شده و به مناسبت بیستمین سالگرد آن بازنویسی شده است. اصول بی‌زمانی را پوشش می‌دهد که هر برنامه‌نویسی باید بداند — از مسئولیت پذیری شخصی و توسعهٔ شغلی تا تکنیک‌های معماری برای انعطاف‌پذیر نگه‌داشتن کد.

---

## سرفصل‌های اصلی

> The book is divided into several topic-based sections covering: A Pragmatic Philosophy, A Pragmatic Approach, The Basic Tools, Pragmatic Paranoia, Bend or Break, Concurrency, While You Are Coding, and Pragmatic Projects.

کتاب به چندین بخش موضوعی تقسیم شده: فلسفهٔ عملگرا، رویکرد عملگرا، ابزارهای پایه، شک‌گرایی عملگرا، انعطاف یا شکست، همزمانی، در حین برنامه‌نویسی، و پروژه‌های عملگرا.

---

## چه کسانی باید این کتاب را بخوانند؟

> Whether you are a beginner or an experienced developer, this book offers valuable insights. It's particularly useful for developers who want to improve their craft and think more deeply about software development practices.

چه مبتدی باشید و چه توسعه‌دهندهٔ با تجربه، این کتاب بینش‌های ارزشمندی ارائه می‌دهد. به‌ویژه برای توسعه‌دهندگانی مفید است که می‌خواهند مهارت خود را بهبود ببخشند و عمیق‌تر دربارهٔ شیوه‌های توسعهٔ نرم‌افزار فکر کنند.

---

## پیش‌گفتار (Foreword)

> I remember when Dave and Andy first tweeted about the new edition of this book. It was big news. I watched as the coding community responded with excitement. My feed buzzed with anticipation. After twenty years, The Pragmatic Programmer is just as relevant today as it was back then.
> It says a lot that a book with such history had such a reaction. I had the privilege of reading an unreleased copy to write this foreword, and I understood why it created such a stir. While it’s a technical book, calling it that does it a disservice. Technical books often intimidate. They’re stuffed with big words, obscure terms, convoluted examples that, unintentionally, make you feel stupid. The more experienced the author, the easier it is to forget what it’s like to learn new concepts, to be a beginner.
> Despite their decades of programming experience, Dave and Andy have conquered the difficult challenge of writing with the same excitement of people who’ve just learned these lessons. They don’t talk down to you. They don’t assume you are an expert. They don’t even assume you’ve read the first edition. They take you as you are—programmers who just want to be better. They spend the pages of this book helping you get there, one actionable step at a time.
> To be fair, they’d already done this before. The original release was full of tangible examples, new ideas, and practical tips to build your coding muscles and develop your coding brain that still apply today. But this updated edition makes two improvements on the book.
> The first is the obvious one: it removes some of the older references, the out-of-date examples, and replaces them with fresh, modern content. You won’t find examples of loop invariants or build machines. Dave and Andy have taken their powerful content and made sure the lessons still come through, free of the distractions of old examples. It dusts off old ideas like DRY (don’t repeat yourself) and gives them a fresh coat of paint, really making them shine.
> But the second is what makes this release truly exciting. After writing the first edition, they had the chance to reflect on what they were trying to say, what they wanted their readers to take away, and how it was being received. They got feedback on those lessons. They saw what stuck, what needed refining, what was misunderstood. In the twenty years that this book has made its way through the hands and hearts of programmers all over the world, Dave and Andy have studied this response and formulated new ideas, new concepts.
> They’ve learned the importance of agency and recognized that developers have arguably more agency than most other professionals. They start this book with the simple but profound message: “it’s your life.” It reminds us of our own power in our code base, in our jobs, in our careers. It sets the tone for everything else in the book—that it’s more than just another technical book filled with code examples.
> What makes it truly stand out among the shelves of technical books is that it understands what it means to be a programmer. Programming is about trying to make the future less painful. It’s about making things easier for our teammates. It’s about getting things wrong and being able to bounce back. It’s about forming good habits. It’s about understanding your toolset. Coding is just part of the world of being a programmer, and this book explores that world.
> I spend a lot of time thinking about the coding journey. I didn’t grow up coding; I didn’t study it in college. I didn’t spend my teenage years tinkering with tech. I entered the coding world in my mid-twenties and had to learn what it meant to be a programmer. This community is very different from others I’d been a part of. There is a unique dedication to learning and practicality that is both refreshing and intimidating.
> For me, it really does feel like entering a new world. A new town, at least. I had to get to know the neighbors, pick my grocery store, find the best coffee shops. It took a while to get the lay of the land, to find the most efficient routes, to avoid the streets with the heaviest traffic, to know when traffic was likely to hit. The weather is different, I needed a new wardrobe.
> The first few weeks, even months, in a new town can be scary. Wouldn’t it be wonderful to have a friendly, knowledgeable neighbor who’d been living there a while? Who can give you a tour, show you those coffee shops? Someone who’d been there long enough to know the culture, understand the pulse of the town, so you not only feel at home, but become a contributing member as well? Dave and Andy are those neighbors.
> As a relative newcomer, it’s easy to be overwhelmed not by the act of programming but the process of becoming a programmer. There is an entire mindset shift that needs to happen—a change in habits, behaviors, and expectations. The process of becoming a better programmer doesn’t just happen because you know how to code; it must be met with intention and deliberate practice. This book is a guide to becoming a better programmer efficiently.
> But make no mistake—it doesn’t tell you how programming should be. It’s not philosophical or judgmental in that way. It tells you, plain and simple, what a Pragmatic Programmer is—how they operate, and how they approach code. They leave it up to you to decide if you want to be one. If you feel it’s not for you, they won’t hold it against you. But if you decide it is, they’re your friendly neighbors, there to show you the way.
> Saron Yitbarek, Founder & CEO of CodeNewbie, Host of Command Line Heroes

یادم می‌آید وقتی دیو و اندی برای اولین بار درباره ویرایش جدید این کتاب توییت کردند. خبر بزرگی بود. دیدم که جامعه برنامه‌نویسان با شور و هیجان واکنش نشان دادند. خوراک من پر از انتظار شده بود. بعد از بیست سال، برنامه‌نویس عملگرا همان‌قدر امروز مرتبط است که آن زمان بود.
خیلی چیزها درباره کتابی با این همه تاریخ می‌گوید که چنین واکنشی ایجاد کرده باشد. من این امتیاز را داشتم که یک نسخه منتشر نشده را برای نوشتن این پیش‌گفتار بخوانم و متوجه شدم چرا این‌قدر جنجال به پا کرد. در حالی که یک کتاب فنی است، فقط فنی خواندن آن بی‌انصافی است. کتاب‌های فنی اغلب ترسناک هستند. پر از کلمات بزرگ، اصطلاحات مبهم، و مثال‌های پیچیده‌اند که ناخودآگاه باعث می‌شوند احساس حماقت کنید. هرچه نویسنده باتجربه‌تر باشد، یادگیری مفاهیم جدید و مبتدی بودن را فراموش می‌کند.
علی‌رغم دهه‌ها تجربه برنامه‌نویسی، دیو و اندی بر چالش دشوار نوشتن با همان هیجان افرادی که تازه این درس‌ها را یاد گرفته‌اند غلبه کرده‌اند. آن‌ها با تحقیر با شما صحبت نمی‌کنند. فرض نمی‌کنند شما متخصص هستید. حتی فرض نمی‌کنند ویرایش اول را خوانده‌اید. شما را همان‌طور که هستید می‌پذیرند — برنامه‌نویسانی که فقط می‌خواهند بهتر شوند. آن‌ها صفحات این کتاب را صرف کمک به شما برای رسیدن به آن هدف می‌کنند، یک قدم عملی در یک زمان.
منصفانه بگوییم، آن‌ها قبلاً هم این کار را کرده بودند. انتشار اصلی پر از مثال‌های عینی، ایده‌های جدید و نکات عملی برای تقویت مهارت‌های برنامه‌نویسی شما بود که هنوز هم امروز کاربرد دارند. اما این ویرایش به‌روزرسانی شده دو بهبود را در کتاب ایجاد می‌کند.
اولین مورد واضح است: برخی ارجاعات قدیمی، مثال‌های قدیمی‌شده را حذف می‌کند و آن‌ها را با محتوای تازه و مدرن جایگزین می‌کند. مثال‌هایی از loop invariants یا build machines پیدا نخواهید کرد. دیو و اندی محتوای قدرتمند خود را گرفته‌اند و مطمئن شده‌اند درس‌ها هنوز منتقل می‌شوند، بدون حواس‌پرتی مثال‌های قدیمی. ایده‌های قدیمی مانند DRY (تکرار نکنید) را تازه می‌کند و واقعاً آن‌ها را می‌درخشد.
اما دومین مورد چیزی است که این انتشار را واقعاً هیجان‌انگیز می‌کند. بعد از نوشتن ویرایش اول، فرصتی برای بازاندیشی در آنچه می‌خواستند بگویند، آنچه می‌خواستند خوانندگان ببرند، و نحوه دریافت آن داشتند. بازخورد دریافت کردند. دیدند چه چیزی ماند، چه چیزی نیاز به ت精细 داشت، و چه چیزی سوءتفاهم شد. در بیست سالی که این کتاب از دست‌ها و دل‌های برنامه‌نویسان در سراسر جهان عبور کرده، دیو و اندی این واکنش را مطالعه کرده و ایده‌ها و مفاهیم جدیدی تدوین کرده‌اند.
آن‌ها اهمیت agency (توانایی عمل) را آموخته‌اند و تشخیص داده‌اند که توسعه‌دهندگان احتمالاً agency بیشتری نسبت به اکثر حرفه‌های دیگر دارند. آن‌ها این کتاب را با پیام ساده اما عمیقی شروع می‌کنند: "این زندگی شماست." این به ما یادآوری می‌کند که قدرت ما در پایگاه کد، شغل و حرفه‌مان چقدر است.
چیزی که واقعاً این کتاب را در میان قفسه‌های کتاب‌های فنی برجسته می‌کند این است که درک می‌کند برنامه‌نویس بودن یعنی چه. برنامه‌نویسی درباره تلاش برای کم‌دردناک‌تر کردن آینده است. درباره آسان‌تر کردن کارها برای هم‌تیمی‌هاست. درباره اشتباه کردن و توانایی بازگشت است. درباره ایجاد عادت‌های خوب است. درباره درک ابزارهایتان است. کدنویسی فقط بخشی از دنیای برنامه‌نویس بودن است و این کتاب آن دنیا را کاوش می‌کند.
من زیاد درباره سفر برنامه‌نویسی فکر می‌کنم. من با کدنویسی بزرگ نشدم؛ آن را در دانشگاه مطالعه نکردم. سال‌های نوجوانی‌ام را با فناوری سروکار نداشتم. در اواسط دهه بیستم وارد دنیای کدنویسی شدم و مجبور بودم بفهمم برنامه‌نویس بودن به چه معناست. این جامعه بسیار متفاوت از جوامع دیگری است که عضوش بودم. فداکاری منحصربه‌فردی برای یادگیری و عمل‌گرایی وجود دارد که هم تازه‌کننده و هم ترسناک است.
برای من، واقعاً مثل ورود به دنیای جدید است. حداقل یک شهر جدید. باید همسایگان را بشناسم، فروشگاه مواد غذایی‌ام را انتخاب کنم، بهترین کافه‌ها را پیدا کنم. مدتی طول کشید تا نقشه زمین را بفهمم، مسیرهای کارآمدتر را پیدا کنم، از خیابان‌های شلوغ اجتناب کنم و بدانم ترافیک چه زمانی اتفاق می‌افتد. هوا متفاوت است، به کمد لباس جدید نیاز دارم.
اولین هفته‌ها، حتی ماه‌ها، در یک شهر جدید ترسناک می‌تواند باشد. چقدر خوب می‌شد اگر یک همسایه خوش‌برخورد و با دانش که مدتی است آنجا زندگی می‌کند داشتید؟ کسی که بتواند تور نشان‌تان دهد، آن کافه‌ها را نشان‌تان دهد؟ کسی که آن‌قدر آنجا بوده باشد که فرهنگ را بشناسد، نبض شهر را درک کند، و شما نه تنها احساس خانه کنید، بلکه عضو مفیدی هم شوید؟ دیو و اندی آن همسایه‌ها هستند.
به عنوان یک تازه‌وارد نسبی، آسان است که نه با خود برنامه‌نویسی، بلکه با فرآیند برنامه‌نویس شدن تحت تأثیر قرار بگیرید. یک تغییر ذهنیت کامل باید اتفاق بیفتد — تغییر در عادت‌ها، رفتارها و انتظارات. فرآیند برنامه‌نویس بهتر شدن فقط به این دلیل اتفاق نمی‌افتد که می‌دانید چگونه کد بزنید؛ باید با نیت و تمرین عمدی همراه باشد. این کتاب راهنمای کارآمد برنامه‌نویس بهتر شدن است.
اما اشتباه نکنید — به شما نمی‌گوید برنامه‌نویسی چگونه باید باشد. فلسفی یا قضاوت‌گرانه نیست. به شما به سادگی می‌گوید برنامه‌نویس عملگرا کیست — چگونه عمل می‌کند و چگونه به کد نزدیک می‌شود. تصمیم با شماست که آیا می‌خواهید یکی از آن‌ها باشید. اگر احساس می‌کنید مناسب شما نیست، شما را قضاوت نمی‌کنند. اما اگر تصمیم بگیرید، همسایگان خوش‌برخورد شما هستند، آماده نشان دادن راه.

---

## پیش‌گفتار ویرایش دوم (Preface to the Second Edition)

> Back in the 1990s, we worked with companies whose projects were having problems. We found ourselves saying the same things to each: maybe you should test that before you ship it; why does the code only build on Mary’s machine? Why didn’t anyone ask the users?
> To save time with new clients, we started jotting down notes. And those notes became The Pragmatic Programmer. To our surprise the book seemed to strike a chord, and it has continued to be popular these last 20 years.
> But 20 years is many lifetimes in terms of software. Take a developer from 1999 and drop them into a team today, and they’d struggle in this strange new world. But the world of the 1990s is equally foreign to today’s developer. The book’s references to things such as CORBA, CASE tools, and indexed loops were at best quaint and more likely confusing.
> At the same time, 20 years has had no impact whatsoever on common sense. Technology may have changed, but people haven’t. Practices and approaches that were a good idea then remain a good idea now. Those aspects of the book aged well.
> So when it came time to create this 20th Anniversary Edition, we had to make a decision. We could go through and update the technologies we reference and call it a day. Or we could reexamine the assumptions behind the practices we recommended in the light of an additional two decades’ worth of experience. In the end, we did both.
> As a result, this book is something of a Ship of Theseus. Roughly one-third of the topics in the book are brand new. Of the rest, the majority have been rewritten, either partially or totally. Our intent was to make things clearer, more relevant, and hopefully somewhat timeless.
> We made some difficult decisions. We dropped the Resources appendix, both because it would be impossible to keep up-to-date and because it’s easier to search for what you want. We reorganized and rewrote topics to do with concurrency, given the current abundance of parallel hardware and the dearth of good ways of dealing with it. We added content to reflect changing attitudes and environments, from the agile movement which we helped launch, to the rising acceptance of functional programming idioms and the growing need to consider privacy and security.
> Interestingly, though, there was considerably less debate between us on the content of this edition than there was when we wrote the first. We both felt that the stuff that was important was easier to identify.
> Anyway, this book is the result. Please enjoy it. Maybe adopt some new practices. Maybe decide that some of the stuff we suggest is wrong. Get involved in your craft. Give us feedback.
> But, most important, remember to make it fun.
> How the Book Is Organized: This book is written as a collection of short topics. Each topic is self-contained, and addresses a particular theme. You’ll find numerous cross references, which help put each topic in context. Feel free to read the topics in any order—this isn’t a book you need to read front-to-back.
> Occasionally you’ll come across a box labeled Tip nn. As well as emphasizing points in the text, we feel the tips have a life of their own—we live by them daily.
> We’ve included exercises and challenges where appropriate. Exercises normally have relatively straightforward answers, while the challenges are more open-ended. To give you an idea of our thinking, we’ve included our answers to the exercises in an appendix, but very few have a single correct solution.

در دهه ۱۹۹۰، با شرکت‌هایی کار می‌کردیم که پروژه‌هایشان مشکل داشت. متوجه شدیم چیزهای یکسانی به همه می‌گوییم: شاید قبل از ارسال آن را تست کنید؛ چرا کد فقط روی ماشین مری کار می‌کند؟ چرا هیچ‌کس از کاربران نپرسید؟
برای صرفه‌جویی در زمان با مشتریان جدید، شروع به یادداشت کردن کردیم. و آن یادداشت‌ها تبدیل به برنامه‌نویس عملگرا شد. به تعجب ما، کتاب ظاهراً هم‌آوایی ایجاد کرد و در ۲۰ سال گذشته محبوبیت خود را حفظ کرده است.
اما ۲۰ سال از نظر نرم‌افزار عمرهای زیادی است. یک توسعه‌دهنده از ۱۹۹۹ را بردارید و در تیم امروز قرار دهید، در این دنیای عجیب جدید مشکل خواهد داشت. اما دنیای دهه ۱۹۹۰ نیز به همان اندازه برای توسعه‌دهنده امروزی ناآشناست. ارجاعات کتاب به چیزهایی مانند CORBA، ابزارهای CASE و حلقه‌های ایندکس‌شده در بهترین حالت عجیب و احتمالاً گیج‌کننده بودند.
در عین حال، ۲۰ سال هیچ تأثیری بر عقل سلیم نداشته است. فناوری ممکن است تغییر کرده باشد، اما انسان‌ها تغییر نکرده‌اند. شیوه‌ها و رویکردهایی که آن زمان ایده خوبی بودند، امروز هم ایده خوبی هستند. آن جنبه‌های کتاب خوب پیر شدند.
بنابراین وقتی زمان ایجاد این ویرایش بیستمین سالگرد فرا رسید، مجبور شدیم تصمیم بگیریم. می‌توانستیم فناوری‌هایی که ارجاع می‌دهیم را به‌روزرسانی کنیم و تمام. یا می‌توانستیم فرضیات پشت شیوه‌هایی که توصیه کرده بودیم را در نور دو دهه تجربه اضافی بازنگری کنیم. در نهایت، هر دو را انجام دادیم.
در نتیجه، این کتاب تا حدودی کشتی تزووس است. تقریباً یک سوم موضوعات کتاب کاملاً جدید هستند. از بقیه، اکثریت بازنویسی شده‌اند، یا جزئی یا کامل. هدف ما روشن‌تر، مرتبط‌تر و امیدوارانه تا حدی بی‌زمان کردن مفاهیم بود.
تصمیم‌های دشواری گرفتیم. پیوست منابع را حذف کردیم، هم به این دلیل که به‌روز نگه داشتن آن غیرممکن بود و هم به این دلیل که جستجوی آنچه می‌خواهید آسان‌تر است. موضوعات مربوط به همزمانی را سازماندهی مجدد و بازنویسی کردیم، با توجه به فراوانی فعلی سخت‌افزار موازی و کمبود راه‌های خوب مقابله با آن. محتوا اضافه کردیم تا نگرش‌ها و محیط‌های در حال تغییر را منعکس کند، از جنبش چالاک که ما در راه‌اندازی آن کمک کردیم، تا پذیرش فزاینده الگوهای برنامه‌نویسی تابعی و نیاز روزافزون به در نظر گرفتن حریم خصوصی و امنیت.
جالب اینجاست که بحث بین ما در مورد محتوای این ویرایش به مراتب کمتر از زمانی بود که ویرایش اول را می‌نوشتیم. هر دو احساس کردیم چیزهای مهم‌تر آسان‌تر قابل شناسایی بودند.
به هر حال، این کتاب نتیجه است. لطفاً لذت ببرید. شاید شیوه‌های جدیدی بپذیرید. شاید تصمیم بگیرید برخی چیزهایی که پیشنهاد می‌کنیم اشتباه است. در حرفه خود درگیر شوید. بازخورد بدهید.
اما مهم‌تر از همه، به یاد داشته باشید که آن را سرگرم‌کننده کنید.

---

## از پیش‌گفتار ویرایش اول (From the Preface to the First Edition)

> This book will help you become a better programmer. You could be a lone developer, a member of a large project team, or a consultant working with many clients at once. It doesn’t matter; this book will help you, as an individual, to do better work. This book isn’t theoretical—we concentrate on practical topics, on using your experience to make more informed decisions. The word pragmatic comes from the Latin pragmaticus—"skilled in business"—which in turn is derived from the Greek πραγματικός, meaning "fit for use."
> This is a book about doing.
> Programming is a craft. At its simplest, it comes down to getting a computer to do what you want it to do (or what your user wants it to do). As a programmer, you are part listener, part advisor, part interpreter, and part dictator. You try to capture elusive requirements and find a way of expressing them so that a mere machine can do them justice. You try to document your work so that others can understand it, and you try to engineer your work so that others can build on it. What’s more, you try to do all this against the relentless ticking of the project clock. You work small miracles every day.
> It’s a difficult job.
> There are many people offering you help. Tool vendors tout the miracles their products perform. Methodology gurus promise that their techniques guarantee results. Everyone claims that their programming language is the best, and every operating system is the answer to all conceivable ills.
> Of course, none of this is true. There are no easy answers. There is no best solution, be it a tool, a language, or an operating system. There can only be systems that are more appropriate in a particular set of circumstances.
> This is where pragmatism comes in. You shouldn’t be wedded to any particular technology, but have a broad enough background and experience base to allow you to choose good solutions in particular situations. Your background stems from an understanding of the basic principles of computer science, and your experience comes from a wide range of practical projects. Theory and practice combine to make you strong.
> You adjust your approach to suit the current circumstances and environment. You judge the relative importance of all the factors affecting a project and use your experience to produce appropriate solutions. And you do this continuously as the work progresses. Pragmatic Programmers get the job done, and do it well.
> Who Should Read This Book? This book is aimed at people who want to become more effective and more productive programmers. Perhaps you feel frustrated that you don’t seem to be achieving your potential. Perhaps you look at colleagues who seem to be using tools to make themselves more productive than you. Maybe your current job uses older technologies, and you want to know how newer ideas can be applied to what you do.
> What Makes a Pragmatic Programmer? Each developer is unique, with individual strengths and weaknesses, preferences and dislikes. Over time, each will craft their own personal environment. That environment will reflect the programmer's individuality just as forcefully as his or her hobbies, clothing, or haircut.
> Early adopter/fast adapter: You have an instinct for technologies and techniques, and you love trying things out.
> Inquisitive: You tend to ask questions. You are a pack rat for little facts, each of which may affect some decision years from now.
> Critical thinker: You rarely take things as given without first getting the facts.
> Realistic: You try to understand the underlying nature of each problem you face.
> Jack of all trades: You try hard to be familiar with a broad range of technologies and environments.
> Care About Your Craft (Tip 1): We feel that there is no point in developing software unless you care about doing it well.
> Think! About Your Work (Tip 2): In order to be a Pragmatic Programmer, we’re challenging you to think about what you’re doing while you’re doing it. This isn’t a one-time audit of current practices—it’s an ongoing critical appraisal of every decision you make, every day, and on every project. Never run on auto-pilot. Constantly be thinking, critiquing your work in real time. The old IBM corporate motto, THINK!, is the Pragmatic Programmer’s mantra.

این کتاب به شما کمک می‌کند برنامه‌نویس بهتری شوید. می‌توانید یک توسعه‌دهنده تنها، عضو یک تیم بزرگ پروژه، یا مشاوری باشید که همزمان با مشتریان زیادی کار می‌کند. مهم نیست؛ این کتاب به شما به عنوان یک فرد کمک می‌کند کار بهتری انجام دهید. این کتاب نظری نیست — ما روی موضوعات عملی تمرکز می‌کنیم، روی استفاده از تجربه شما برای تصمیم‌گیری آگاهانه‌تر. کلمه "pragmatic" (عملگرا) از لاتین pragmaticus به معنای "ماهر در کسب‌وکار" آمده که خود از یونانی πραγματιکός به معنای "مناسب برای استفاده" گرفته شده است.
این کتابی درباره عمل کردن است.
برنامه‌نویسی یک حرفه (craft) است. در ساده‌ترین حالت، به انجام کاری توسط کامپیوتر ختم می‌شود که شما می‌خواهید (یا کاربر شما می‌خواهد). به عنوان یک برنامه‌نویس، شما همزمان شنونده، مشاور، مترجم و دیکتاتور هستید. سعی می‌کنید نیازهای دست‌نیافتنی را ثبت کنید و راهی برای بیان آن‌ها بیابید تا یک ماشین ساده بتواند از عهده آن‌ها بربیاید. سعی می‌کنید کارتان را مستند کنید تا دیگران بتوانند درک کنند، و سعی می‌کنید کارتان را مهندسی کنید تا دیگران بتوانند روی آن بنا کنند. علاوه بر این، سعی می‌کنید همه این‌ها را در برابر تیک‌تیک بی‌امان ساعت پروژه انجام دهید. هر روز معجزه‌های کوچکی خلق می‌کنید.
کار دشواری است.
افراد زیادی هستند که کمک شما را می‌کنند. فروشندگان ابزار، معجزه‌های محصولاتشان را تبلیغ می‌کنند. متخصصان روش‌شناسی قول می‌دهند تکنیک‌هایشان نتایج را تضمین می‌کند. همه ادعا می‌کنند زبان برنامه‌نویسیشان بهترین است و هر سیستم‌عاملی پاسخ تمام مشکلات قابل تصور است.
البته، هیچ‌کدام از این‌ها درست نیست. پاسخ آسانی وجود ندارد. بهترین راه‌حلی وجود ندارد، چه ابزار باشد، چه زبان، چه سیستم‌عامل. فقط سیستم‌هایی می‌توانند باشند که در مجموعه خاصی از شرایط مناسب‌تر هستند.
اینجاست که عمل‌گرایی وارد می‌شود. نباید به هیچ فناوری خاصی وابسته باشید، اما باید پیشینه و تجربه کافی گسترده داشته باشید تا بتوانید در شرایط خاص راه‌حل‌های خوبی انتخاب کنید. پیشینه شما از درک اصول پایه علوم کامپیوتر نشأت می‌گیرد و تجربه شما از طیف وسیعی از پروژه‌های عملی می‌آید. نظریه و عمل با هم ترکیب می‌شوند تا شما را قوی کنند.
رویکرد خود را متناسب با شرایط و محیط فعلی تنظیم می‌کنید. اهمیت نسبی تمام عوامل مؤثر بر یک پروژه را قضاوت می‌کنید و از تجربه خود برای تولید راه‌حل‌های مناسب استفاده می‌کنید. و این کار را به طور مداوم در طول پیشرفت کار انجام می‌دهید. برنامه‌نویسان عملگرا کار را انجام می‌دهند و آن را خوب انجام می‌دهند.
چه کسانی باید این کتاب را بخوانند؟ این کتاب برای افرادی است که می‌خواهند برنامه‌نویسان کارآمدتر و مولدتری شوند.
ویژگی‌های برنامه‌نویس عملگرا:
- پذیرنده زودهنگام/سازگار سریع: غریزه‌ای برای فناوری‌ها و تکنیک‌ها دارید و عاشق آزمایش کردن هستید.
- کنجکاو: تمایل دارید سؤال بپرسید. شما یک جمع‌کننده حقایق کوچک هستید.
- متفکر انتقادی: به ندرت چیزها را بدون کسب حقایق قبول می‌کنید.
- واقع‌بین: سعی می‌کنید ماهیت زیربنایی هر مشکلی را درک کنید.
- همه‌فن‌حریف: سعی می‌کنید با طیف وسیعی از فناوری‌ها و محیط‌ها آشنا شوید.
- به حرفه‌ات اهمیت بده (نکته ۱): ما احساس می‌کنیم توسعه نرم‌افزار فایده‌ای ندارد مگر اینکه به انجام خوب آن اهمیت بدهید.
- فکر کن! درباره کارت (نکته ۲): برای اینکه برنامه‌نویس عملگرا باشید، از شما می‌خواهیم درباره آنچه انجام می‌دهید فکر کنید. این یک بار حسابرسی شیوه‌های فعلی نیست — ارزیابی انتقادی مداوم هر تصمیمی است که هر روز و در هر پروژه می‌گیرید. هرگز روی حالت خودکار اجرا نکنید.

---

# فصل اول: فلسفهٔ عملگرا ⏱️ ۲۵ دقیقه مطالعه

## ۱. زندگی شماست (It's Your Life)

> I’m not in this world to live up to your expectations and you’re not in this world to live up to mine.
> ➤ Bruce Lee
>
> It is your life. You own it. You run it. You create it.
> Many developers we talk to are frustrated. Their concerns are varied. Some feel they’re stagnating in their job, others that technology has passed them by. Folks feel they are under appreciated, or underpaid, or that their teams are toxic. Maybe they want to move to Asia, or Europe, or work from home. And the answer we give is always the same. "Why can’t you change it?"
> Software development must appear close to the top of any list of careers where you have control. Our skills are in demand, our knowledge crosses geographic boundaries, we can work remotely. We’re paid well. We really can do just about anything we want.
> But, for some reason, developers seem to resist change. They hunker down, and hope things will get better. They look on, passively, as their skills become dated and complain that their companies don’t train them. They look at ads for exotic locations on the bus, then step off into the chilling rain and trudge into work.
> So here’s the most important tip in the book.
> You Have Agency (Tip 3): Does your work environment suck? Is your job boring? Try to fix it. But don’t try forever. As Martin Fowler says, "you can change your organization or change your organization."

من در این دنیا نیستم که انتظارات شما را برآورده کنم و شما هم در این دنیا نیستید که انتظارات مرا برآورده کنید.
زندگی شماست. مال شماست. اداره‌اش می‌کنید. خلقش می‌کنید.
بسیاری از توسعه‌دهندگانی که با آن‌ها صحبت می‌کنیم ناامید هستند. نگرانی‌هایشان متفاوت است. برخی احساس می‌کنند در شغلشان راکد شده‌اند، برخی دیگر احساس می‌کنند فناوری از آن‌ها عقب افتاده است. برخی احساس می‌کنند قدردانی نمی‌شوند، یا حقوق کمی می‌گیرند، یا تیم‌هایشان سمی است. شاید می‌خواهند به آسیا یا اروپا نقل مکان کنند، یا از خانه کار کنند. و پاسخی که ما می‌دهیم همیشه یکسان است: "چرا نمی‌توانید آن را تغییر دهید؟"
توسعه نرم‌افزار باید در بالای هر لیستی از مشاغلی باشد که در آن کنترل دارید. مهارت‌های ما مورد تقاضا هستند، دانش ما از مرزهای جغرافیایی عبور می‌کند، می‌توانیم از راه کار کنیم. خوب حقوق می‌گیریم. واقعاً می‌توانیم تقریباً هر کاری که بخواهیم انجام دهیم.
اما به دلیلی، توسعه‌دهندگان ظاهراً در برابر تغییر مقاومت می‌کنند. سنگر می‌گیرند و امیدوارند همه‌چیز بهتر شود. منفعلانه نگاه می‌کنند، در حالی که مهارت‌هایشان قدیمی می‌شود و شکایت می‌کنند که شرکت‌هایشان آموزش نمی‌دهد.
پس این مهم‌ترین نکته کتاب است: شما توانایی عمل دارید (نکته ۳). محیط کارتان بد است؟ شغلتان کسل‌کننده است؟ سعی کنید آن را تغییر دهید. اما برای همیشه تلاش نکنید. همان‌طور که مارتین فاولر می‌گوید: "می‌توانید سازمان‌تان را تغییر دهید یا سازمان‌تان را تغییر دهید."

---

## ۲. گربه کد منبعم را خورد (The Cat Ate My Source Code)

> The greatest of all weaknesses is the fear of appearing weak.
> ➤ J.B. Bossuet, Politics from Holy Writ, 1709
>
> One of the cornerstones of the pragmatic philosophy is the idea of taking responsibility for yourself and your actions in terms of your career advancement, your learning and education, your project, and your day-to-day work. Pragmatic Programmers take charge of their own career, and aren’t afraid to admit ignorance or error.
> Team Trust: Above all, your team needs to be able to trust and rely on you—and you need to be comfortable relying on each of them as well.
> Take Responsibility: Responsibility is something you actively agree to. You make a commitment to ensure that something is done right, but you don’t necessarily have direct control over every aspect of it.
> Provide Options, Don’t Make Lame Excuses (Tip 4): Before you approach anyone to tell them why something can’t be done, is late, or is broken, stop and listen to yourself. Instead of excuses, provide options. Don’t say it can’t be done; explain what can be done to salvage the situation.

بزرگ‌ترین ضعف‌ها، ترس از به نظر رسیدن ضعیف است.
یکی از سنگ‌بنای‌های فلسفه عملگرا ایده پذیرش مسئولیت برای خود و اعمالتان است — از پیشرفت حرفه‌ای، یادگیری و تحصیلات، پروژه و کار روزانه‌تان. برنامه‌نویسان عملگرا مدیریت حرفه خود را بر عهده می‌گیرند و از اعتراف به ناآگاهی یا خطا نمی‌ترسند.
اعتماد تیم: مهم‌تر از همه، تیم شما باید بتواند به شما اعتماد کند و روی شما حساب کند — و شما هم باید راحت باشید که روی هر کدام از آن‌ها حساب کنید.
مسئولیت بپذیرید: مسئولیت چیزی است که فعالانه با آن موافقت می‌کنید. تعهد می‌دهید که کاری درست انجام شود، اما لزوماً کنترل مستقیمی بر هر جنبه آن ندارید.
گزینه‌ها ارائه دهید، بهانه‌های ضعیف نیاورید (نکته ۴): قبل از اینکه به کسی بگویید چرا کاری قابل انجام نیست، دیر شده، یا خراب است، متوقف شوید و به خودتان گوش دهید. به جای بهانه، گزینه‌ها ارائه دهید. نگویید قابل انجام نیست؛ توضیح دهید چه کاری می‌توان برای نجات موقعیت انجام داد.

---

## ۳. آنتروپی نرم‌افزار (Software Entropy)

> While software development is immune from almost all physical laws, the inexorable increase in entropy hits us hard. Entropy is a term from physics that refers to the amount of "disorder" in a system. When disorder increases in software, we call it "software rot."
> A broken window: One broken window, left unrepaired for any substantial length of time, instills in the inhabitants of the building a sense of abandonment.
> Don’t Live with Broken Windows (Tip 5): Don’t leave "broken windows" (bad designs, wrong decisions, or poor code) unrepaired. Fix each one as soon as it is discovered.
> First, Do No Harm: Don’t cause collateral damage just because there’s a crisis of some sort. One broken window is one too many.

در حالی که توسعه نرم‌افزار از تقریباً تمام قوانین فیزیکی مصون است، افزایش غیرقابل اجتناب آنتروپی ما را سخت می‌زند. آنتروپی اصطلاحی از فیزیک است که به میزان "بی‌نظمی" در یک سیستم اشاره دارد. وقتی بی‌نظمی در نرم‌افزار افزایش می‌یابد، آن را "پوسیدگی نرم‌افزار" می‌نامیم.
پنجره شکسته: یک پنجره شکسته، اگر برای مدت قابل توجهی تعمیر نشود، در ساکنان ساختمان احساس رها شدن ایجاد می‌کند.
با پنجره‌های شکسته زندگی نکنید (نکته ۵): "پنجره‌های شکسته" (طراحی‌های بد، تصمیمات اشتباه، یا کد ضعیف) را تعمیر نشده رها نکنید. هر کدام را به محض کشف تعمیر کنید.
اول، آسیب نزنید: فقط به این دلیل که بحرانی وجود دارد، خسارت جانبی ایجاد نکنید. یک پنجره شکسته هم زیاد است.

---

## ۴. سوپ سنگی و قورباغه‌های آب‌پز (Stone Soup and Boiled Frogs)

> The three soldiers returning home from war were hungry. When they saw the village ahead their spirits lifted—they were sure the villagers would give them a meal. But when they got there, they found the doors locked and the windows closed. The soldiers boiled a pot of water and carefully placed three stones into it.
> The villagers are tricked by the soldiers, who use the villagers' curiosity to get food from them. But more importantly, the soldiers act as a catalyst, bringing the village together so they can jointly produce something that they couldn't have done by themselves—a synergistic result.
> Be a Catalyst for Change (Tip 6): Work out what you can reasonably ask for. Develop it well. Once you've got it, show people, and let them marvel.
> The Villagers' Side: Things just creep up on us. Projects slowly and inexorably get totally out of hand. Most software disasters start out too small to notice.
> Remember the Big Picture (Tip 7): Don't be like the fabled frog. Keep an eye on the big picture. Constantly review what's happening around you, not just what you personally are doing.

سه سرباز که از جنگ به خانه بازمی‌گشتند گرسنه بودند. وقتی روستا را در پیش رو دیدند روحیه‌شان بالا رفت — مطمئن بودند اهالی روستا به آن‌ها غذا خواهند داد. اما وقتی رسیدند، درها قفل و پنجره‌ها بسته بود. سربازان قابلمه‌ای آب جوشاندند و با دقت سه سنگ در آن انداختند.
اهالی روستا توسط سربازان فریب می‌خورند، که از کنجکاوی آن‌ها برای گرفتن غذا استفاده می‌کنند. اما مهم‌تر از آن، سربازان به عنوان کاتالیزور عمل می‌کنند و روستا را گرد هم می‌آورند تا بتوانند با هم چیزی تولید کنند که به تنهایی نمی‌توانستند — نتیجه‌ای هم‌افزا.
کاتالیزور تغییر باشید (نکته ۶): چیزی که می‌توانید معقولانه درخواست کنید را مشخص کنید. آن را خوب توسعه دهید. وقتی آماده شد، به مردم نشان دهید و بگذارید شگفت‌زده شوند.
سمت اهالی روستا: چیزها آهسته به ما نزدیک می‌شوند. پروژه‌ها آهسته و به طور غیرقابل اجتناب از کنترل خارج می‌شوند.
تصویر بزرگ را به یاد داشته باشید (نکته ۷): مثل قورباغه افسانه‌ای نباشید. تصویر بزرگ را زیر نظر داشته باشید. مدام بررسی کنید چه اتفاقی در اطرافتان می‌افتد، نه فقط آنچه شما شخصاً انجام می‌دهید.

---

## ۵. نرم‌افزار خوب enough (Good-Enough Software)

> Striving to better, oft we mar what’s well.
> ➤ Shakespeare, King Lear 1.4
>
> When good-enough software is best, you can discipline yourself to write software that’s good enough—good enough for your users, for future maintainers, for your own peace of mind.
> Make Quality a Requirements Issue (Tip 8): Often you’ll be in situations where trade-offs are involved. Many users would rather use software with some rough edges today than wait a year for the shiny version. Great software today is often preferable to the fantasy of perfect software tomorrow.
> Know When to Stop: In some ways, programming is like painting. You start with a blank canvas and certain basic raw materials. But artists will tell you that all the hard work is ruined if you don’t know when to stop.

تلاش برای بهتر شدن، اغلب آنچه خوب است را خراب می‌کند.
وقتی نرم‌افزار خوب enough بهترین گزینه است، می‌توانید به خودتان انضباط بدهید تا نرم‌افزاری بنویسید که خوب enough باشد — خوب enough برای کاربرانتان، برای نگه‌دارندگان آینده، برای آرامش خودتان.
کیفیت را یک مسئله نیازمندی بدانید (نکته ۸): اغلب در موقعیت‌هایی خواهید بود که مبادلاتی در کار است. بسیاری از کاربران ترجیح می‌دهند امروز نرم‌افزاری با برخی ناهمواری‌ها استفاده کنند تا اینکه یک سال برای نسخه براق صبر کنند. نرم‌افزار عالی امروز اغلب بر تصور نرم‌افزار فردا ترجیح دارد.
بدانید چه زمانی متوقف شوید: از جهاتی، برنامه‌نویسی مثل نقاشی است. با بوم خالی و مواد اولیه پایه شروع می‌کنید. اما هنرمندان به شما می‌گویند تمام تلاش‌ها خراب می‌شود اگر ندانید چه زمانی متوقف شوید.

---

## ۶. سبد دانش شما (Your Knowledge Portfolio)

> An investment in knowledge always pays the best interest.
> ➤ Benjamin Franklin
>
> Your knowledge and experience are your most important day-to-day professional assets. Unfortunately, they’re expiring assets.
> Managing a knowledge portfolio is very similar to managing a financial portfolio:
> 1. Serious investors invest regularly—as a habit.
> 2. Diversification is the key to long-term success.
> 3. Smart investors balance their portfolios between conservative and high-risk, high-reward investments.
> 4. Investors try to buy low and sell high for maximum return.
> 5. Portfolios should be reviewed and rebalanced periodically.
> Invest Regularly in Your Knowledge Portfolio (Tip 9): Learn at least one new language every year. Read a technical book each month. Read nontechnical books too. Take classes. Participate in local user groups and meetups. Experiment with different environments. Stay current.
> Critically Analyze What You Read and Hear (Tip 10): Ask the "Five Whys." Who does this benefit? What's the context?

سرمایه‌گذاری در دانش همیشه بهترین سود را می‌دهد.
دانش و تجربه شما مهم‌ترین دارایی‌های حرفه‌ای روزانه شما هستند. متأسفانه، دارایی‌هایی با تاریخ انقضا هستند.
مدیریت سبد دانش بسیار شبیه مدیریت سبد مالی است:
۱. سرمایه‌گذاران جدی منظم سرمایه‌گذاری می‌کنند — به عنوان یک عادت.
۲. تنوع کلید موفقیت بلندمدت است.
۳. سرمایه‌گذاران هوشمند سبد خود را بین سرمایه‌گذاری‌های محافظه‌کارانه و پرریسک متعادل می‌کنند.
۴. سرمایه‌گذاران سعی می‌کنند ارزان بخرند و گران بفروشند.
۵. سبدها باید دوره‌ای بازنگری و متعادل شوند.
منظم در سبد دانش خود سرمایه‌گذاری کنید (نکته ۹): هر سال حداقل یک زبان جدید یاد بگیرید. هر ماه یک کتاب فنی بخوانید. کتاب‌های غیرفنی هم بخوانید. در کلاس‌ها شرکت کنید. در گروه‌های کاربری محلی شرکت کنید. با محیط‌های مختلف آزمایش کنید.
آنچه می‌خوانید و می‌شنوید را به طور انتقادی تحلیل کنید (نکته ۱۰): "چرای پنجگانه" را بپرسید. این به نفع کیست؟ زمینه چیست؟

---

## ۷. ارتباط برقرار کن! (Communicate!)

> I believe that it is better to be looked over than it is to be overlooked.
> ➤ Mae West, Belle of the Nineties, 1934
>
> Maybe we can learn a lesson from Ms. West. It’s not just what you’ve got, but also how you package it. Having the best ideas, the finest code, or the most pragmatic thinking is ultimately sterile unless you can communicate with other people. A good idea is an orphan without effective communication.
> English is Just Another Programming Language (Tip 11): Treat English (or whatever your native tongue may be) as just another programming language.
> Know Your Audience: You’re communicating only if you’re conveying what you mean to convey—just talking isn’t enough.
> Know What You Want to Say: Plan what you want to say. Write an outline.
> Choose Your Moment: Work out what their priorities are. Make what you’re saying relevant in time, as well as in content.
> Choose a Style: Adjust the style of your delivery to suit your audience.
> Make It Look Good: Your ideas are important. They deserve a good-looking vehicle to convey them to your audience.
> Involve Your Audience: If possible, involve your readers with early drafts of your document.
> Be a Listener: If you want people to listen to you: listen to them.
> Get Back to People: Always respond to emails and voicemails, even if the response is simply "I'll get back to you later."
> It’s Both What You Say and the Way You Say It (Tip 12): The more effective that communication, the more influential you become.
> Build Documentation In, Don’t Bolt It On (Tip 13): It’s easy to produce good-looking documentation from the comments in source code.

شاید بتوانیم درسی از خانم وست بگیریم. مهم فقط آن چیزی نیست که دارید، بلکه نحوه بسته‌بندی آن هم هست. داشتن بهترین ایده‌ها، بهترین کد، یا عمل‌گرایانه‌ترین تفکر در نهایت بی‌اثر است مگر اینکه بتوانید با دیگران ارتباط برقرار کنید. یک ایده خوب بدون ارتباطات مؤثر یتیم است.
انگلیسی فقط یک زبان برنامه‌نویسی دیگر است (نکته ۱۱): با انگلیسی (یا هر زبان مادری دیگری) مثل یک زبان برنامه‌نویسی دیگر رفتار کنید.
مخاطب خود را بشناسید: فقط وقتی ارتباط برقرار می‌کنید که منظورتان را منتقل می‌کنید — فقط حرف زدن کافی نیست.
بدانید چه می‌خواهید بگویید: آنچه می‌خواهید بگویید را برنامه‌ریزی کنید. یک طرح بنویسید.
لحظه خود را انتخاب کنید: اولویت‌های آن‌ها را مشخص کنید.
سبک را انتخاب کنید: سبک ارائه خود را متناسب با مخاطبتان تنظیم کنید.
خوب به نظر برسد: ایده‌های شما مهم هستند.
مخاطب خود را درگیر کنید: در صورت امکان، خوانندگان را با پیش‌نویس‌های اولیه درگیر کنید.
شنونده باشید: اگر می‌خواهید مردم به شما گوش دهید: به آن‌ها گوش دهید.
به مردم پاسخ دهید: همیشه به ایمیل‌ها و پیام‌های صوتی پاسخ دهید.
هم آنچه می‌گویید و هم نحوه گفتن آن مهم است (نکته ۱۲): هرچه ارتباط مؤثرتر باشد، تأثیرگذارتر می‌شوید.
مستندات را درون کد بسازید، نه اینکه بعداً اضافه کنید (نکته ۱۳): تولید مستندات خوب از نظرات درون کد آسان است.

---

# فصل دوم: رویکرد عملگرا ⏱️ ۲۰ دقیقه مطالعه

## ۸. ماهیت طراحی خوب (The Essence of Good Design)

> Good Design Is Easier to Change Than Bad Design (Tip 14): A thing is well designed if it adapts to the people who use it. For code, that means it must adapt by changing. So we believe in the ETC principle: Easier to Change. ETC. That's it.
> As far as we can tell, every design principle out there is a special case of ETC. Why is decoupling good? Because by isolating concerns we make each easier to change. ETC. Why is the single responsibility principle useful? Because a change in requirements is mirrored by a change in just one module. ETC. Why is naming important? Because good names make code easier to read, and you have to read it to change it. ETC!
> ETC Is a Value, Not a Rule: Values are things that help you make decisions. When it comes to thinking about software, ETC is a guide, helping you choose between paths.

طراحی خوب تغییر آن بد است آسان‌تر است (نکته ۱۴): یک چیز خوب طراحی شده است اگر با افرادی که از آن استفاده می‌کنند سازگار شود. برای کد، این به این معنی است که باید با تغییر سازگار شود. پس ما به اصل ETC اعتقاد داریم: آسان‌تر برای تغییر. ETC. همین.
به نظر ما، هر اصل طراحی‌ای که وجود دارد حالت خاصی از ETC است. چرا جداسازی خوب است؟ چون با جدا کردن نگرانی‌ها، هر کدام را آسان‌تر برای تغییر می‌کنیم. ETC. چرا اصل مسئولیت واحد مفید است؟ چون تغییر در نیازمندی‌ها فقط در یک ماژول منعکس می‌شود. ETC. چرا نام‌گذاری مهم است؟ چون نام‌های خوب کد را آسان‌تر برای خواندن می‌کنند و باید بخوانیدش تا تغییرش دهید. ETC!
ETC یک ارزش است، نه یک قاعده: ارزش‌ها چیزهایی هستند که به شما در تصمیم‌گیری کمک می‌کنند.

---

## ۹. DRY — شرارت‌های تکرار (DRY—The Evils of Duplication)

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.
> DRY—Don't Repeat Yourself (Tip 15): The alternative is to have the same thing expressed in two or more places. If you change one, you have to remember to change the others, or your program will be brought to its knees by a contradiction.
> DRY Is More Than Code: DRY is about the duplication of knowledge, of intent. It's about expressing the same thing in two different places, possibly in two totally different ways.
> Not All Code Duplication Is Knowledge Duplication: The code is the same, but the knowledge they represent is different. The two functions validate two separate things that just happen to have the same rules. That's a coincidence, not a duplication.
> Make It Easy to Reuse (Tip 16): What you're trying to do is foster an environment where it's easier to find and reuse existing stuff than to write it yourself.

هر قطعه دانش باید یک نمایش واحد، غیرمبهم و معتبر درون یک سیستم داشته باشد.
DRY — تکرار نکنید (نکته ۱۵): جایگزین این است که یک چیز در دو یا چند جا بیان شده باشد. اگر یکی را تغییر دهید، باید به یاد داشته باشید بقیه را هم تغییر دهید، وگرنه برنامه‌تان با تناقض زمین می‌خورد.
DRY فقط کد نیست: DRY درباره تکرار دانش، نیت است. درباره بیان یک چیز در دو جای مختلف است، احتمالاً به دو روش کاملاً متفاوت.
هر تکرار کدی تکرار دانش نیست: کد یکسان است، اما دانشی که نشان می‌دهند متفاوت است.
استفاده مجدد را آسان کنید (نکته ۱۶): هدف شما ایجاد محیطی است که در آن پیدا کردن و استفاده مجدد از چیزهای موجود آسان‌تر از نوشتن خودتان باشد.

---

## ۱۰. قطعیت (Orthogonality)

> Orthogonality is a critical concept if you want to produce systems that are easy to design, build, test, and extend. In computing, the term has come to signify a kind of independence or decoupling. Two or more things are orthogonal if changes in one do not affect any of the others.
> Eliminate Effects Between Unrelated Things (Tip 17): We want to design components that are self-contained: independent, and with a single, well-defined purpose.
> Benefits of Orthogonality:
> - Gain Productivity: Changes are localized, so development time and testing time are reduced.
> - Reduce Risk: Diseased sections of code are isolated. The resulting system is less fragile.
> Keep your code decoupled. Write shy code—modules that don't reveal anything unnecessary to other modules.

قطعیت مفهومی حیاتی است اگر می‌خواهید سیستم‌هایی تولید کنید که طراحی، ساخت، تست و گسترش آن‌ها آسان باشد. در محاسبات، این اصطلاح به نوعی استقلال یا جداسازی اشاره کرده است.
اثرات بین چیزهای نامرتبط را حذف کنید (نکته ۱۷): می‌خواهیم مولفه‌هایی طراحی کنیم که خودکفا باشند: مستقل، و با هدف واحد و مشخص.
مزایای قطعیت:
- بهره‌وری افزایش می‌یابد: تغییرات محلی هستند، بنابراین زمان توسعه و تست کاهش می‌یابد.
- ریسک کاهش می‌یابد: بخش‌های آلوده کد جدا می‌شوند. سیستم حاصل شکننده‌تر است.
کدتان را جدا نگه دارید. کد خجالتی بنویسید — ماژول‌هایی که چیز غیرضروری به ماژول‌های دیگر نشان نمی‌دهند.

---

## ۱۱. بازگشت‌پذیری (Reversibility)

> Nothing is more dangerous than an idea if it’s the only one you have.
> ➤ Emil-Auguste Chartier (Alain)
>
> There Are No Final Decisions (Tip 18): Many of the topics in this book are geared to producing flexible, adaptable software. By sticking to their recommendations—especially the DRY principle, decoupling, and use of external configuration—we don't have to make as many critical, irreversible decisions.
> Flexible Architecture: How can you plan for architectural volatility? You can't. What you can do is make it easy to change. Hide third-party APIs behind your own abstraction layers.
> Forgo Following Fads (Tip 19): No one knows what the future may hold, especially not us! So enable your code to rock-n-roll.

هیچ چیز خطرناک‌تر از یک ایده نیست اگر تنها ایده‌ای باشد که دارید.
هیچ تصمیم نهایی وجود ندارد (نکته ۱۸): بسیاری از موضوعات این کتاب برای تولید نرم‌افزار انعطاف‌پذیر و سازگار هستند. با پایبندی به توصیه‌های آن‌ها — به ویژه اصل DRY، جداسازی و استفاده از پیکربندی خارجی — مجبور نیستیم تصمیمات حیاتی و غیرقابل بازگشت زیادی بگیریم.
معماری انعطاف‌پذیر: چگونه برای نوسانات معماری برنامه‌ریزی کنید؟ نمی‌توانید. کاری که می‌توانید انجام دهید این است که تغییر را آسان کنید.
از ترند‌ها پیروی نکنید (نکته ۱۹): هیچ‌کس نمی‌داند آینده چه خواهد داشت، مخصوصاً ما! پس به کدتان اجازه رقص بدهید.

---

## ۱۲. گلوله‌های ردیاب (Tracer Bullets)

> Ready, fire, aim…
> ➤ Anon
>
> Use Tracer Bullets to Find the Target (Tip 20): In fact, given the complexity of today's project setup, with swarms of external dependencies and tools, tracer bullets become even more important.
> Tracer code is not disposable: you write it for keeps. It contains all the error checking, structuring, documentation, and self-checking that any piece of production code has. It simply is not fully functional.
> Tracer Bullets Don't Always Hit Their Target: Tracer bullets show what you're hitting. This may not always be the target. You then adjust your aim until they're on target.
> Tracer Code versus Prototyping: Prototyping generates disposable code. Tracer code is lean but complete, and forms part of the skeleton of the final system.

آماده، شلیک، هدف‌گیری…
از گلوله‌های ردیاب برای یافتن هدف استفاده کنید (نکته ۲۰): در واقع، با توجه به پیچیدگی تنظیمات پروژه‌های امروزی، با انبوهی از وابستگی‌ها و ابزارهای خارجی، گلوله‌های ردیاب حتی مهم‌تر می‌شوند.
کد ردیاب قابل دور ریختن نیست: آن را برای همیشه می‌نویسید. تمام بررسی‌های خطا، ساختاربندی، مستندات و خودبررسی را دارد.
گلوله‌های ردیاب همیشه به هدف نمی‌خورند: گلوله‌های ردیاب نشان می‌دهند به چه چیزی می‌خورید. این ممکن است همیشه هدف نباشد. سپس هدف‌گیری خود را تنظیم می‌کنید.
کد ردیاب در مقابل پروتوتایپ: پروتوتایپ کد قابل دور ریختن تولید می‌کند. کد ردیاب لاغر اما کامل است و بخشی از اسکلت سیستم نهایی را تشکیل می‌دهد.

---

## ۱۳. پروتوتایپ‌ها و یادداشت‌های پست‌ایت (Prototypes and Post-it Notes)

> Many industries use prototypes to try out specific ideas; prototyping is much cheaper than full-scale production.
> Prototype to Learn (Tip 21): Prototyping is a learning experience. Its value lies not in the code produced, but in the lessons learned.
> Things to Prototype: Architecture, new functionality, structure or contents of external data, third-party tools or components, performance issues, user interface design.
> How to Use Prototypes: Ignore correctness, completeness, robustness, and style. Prototypes gloss over details, and focus in on specific aspects of the system.
> How Not to Use Prototypes: Before you embark on any code-based prototyping, make sure that everyone understands that you are writing disposable code.

بسیاری از صنایع از پروتوتایپ‌ها برای آزمایش ایده‌های خاص استفاده می‌کنند؛ پروتوتایپ‌سازی بسیار ارزان‌تر از تولید تمام‌عیار است.
برای یادگیری پروتوتایپ بسازید (نکته ۲۱): پروتوتایپ‌سازی یک تجربه یادگیری است. ارزش آن نه در کد تولید شده، بلکه در درس‌های آموخته شده است.
چیزهایی برای پروتوتایپ: معماری، عملکرد جدید، ساختار یا محتوای داده‌های خارجی، ابزارهای یا مولفه‌های شخص ثالث، مسائل عملکرد، طراحی رابط کاربری.
نحوه استفاده از پروتوتایپ‌ها: از صحت، کامل بودن، استحکام و سبک چشم‌پوشی کنید.
نحوه عدم استفاده از پروتوتایپ‌ها: قبل از شروع هر پروتوتایپ‌سازی مبتنی بر کد، مطمئن شوید همه درک می‌کنند که کد قابل دور ریختن می‌نویسید.

---

## ۱۴. زبان‌های دامنه (Domain Languages)

> The limits of my language are the limits of my world.
> ➤ Ludwig Wittgenstein
>
> Much as you may like to just say "make it so" and have the computer build your application, in many cases you can get at least partway there. Use and build domain languages.
> Domain-Specific Languages (Tip 22): Programming in a small, domain-specific language is often simpler and more natural than programming in a general-purpose language.

محدودیت‌های زبان من، محدودیت‌های دنیای من است.
زبان‌های خاص دامنه (نکته ۲۲): برنامه‌نویسی در یک زبان کوچک و خاص دامنه اغلب ساده‌تر و طبیعی‌تر از برنامه‌نویسی در یک زبان عمومی است.

---

## ۱۵. تخمین (Estimating)

> Estimating is the process of finding an approximation, which is a value that is usable for some purpose even if input data may be incomplete, uncertain, or unstable.
> The Computer Delivers Pizza (Tip 23): Often, when estimating time to do technical tasks, the answer is a complex function of many variables.
> Estimate the Scope of the Work: Break the problem down into smaller pieces. Each component is easier to estimate, and you can add up the estimates.
> Build Estimates from the Bottom Up: Start with the small tasks, and add them up.
> Know When to Leave It Alone: Don't spend too much time on the estimate. It's an approximation, not a commitment.

تخمین فرآیند یافتن تقریبی است که مقداری است که برای برخی اهداف قابل استفاده است حتی اگر داده‌های ورودی ناقص، نامطمئن یا ناپایدار باشند.
کامپیوتر پیتزا تحویل می‌دهد (نکته ۲۳): اغلب، هنگام تخمین زمان برای انجام وظایف فنی، پاسخ تابع پیچیده‌ای از متغیرهای زیادی است.
دامنه کار را تخمین بزنید: مشکل را به قطعات کوچکتر تقسیم کنید.
تخمین‌ها را از پایین به بالا بسازید: با وظایف کوچک شروع کنید و آن‌ها را جمع کنید.
بدانید چه زمانی رهایش کنید: وقت زیادی برای تخمین صرف نکنید.

---

# فصل سوم: ابزارهای پایه ⏱️ ۲۰ دقیقه مطالعه

## ۱۶. قدرت متن ساده (The Power of Plain Text)

> As Pragmatic Programmers, our base material isn't wood or iron, it's knowledge. We gather requirements as knowledge, and then express that knowledge in our designs, implementations, tests, and documents. And we believe that the best format for storing knowledge persistently is plain text.
> Keep Knowledge in Plain Text (Tip 25): With plain text, we give ourselves the ability to manipulate knowledge, both manually and programmatically, using virtually every tool at our disposal.
> Insurance Against Obsolescence: Human-readable forms of data, and self-describing data, will outlive all other forms of data and the applications that created them.
> Leverage: Virtually every tool in the computing universe can operate on plain text.

به عنوان برنامه‌نویسان عملگرا، ماده پایه ما نه چوب و نه آهن است، بلکه دانش است. دانش را به عنوان نیازمندی جمع‌آوری می‌کنیم و سپس آن دانش را در طراحی‌ها، پیاده‌سازی‌ها، تست‌ها و مستندات بیان می‌کنیم. و ما معتقدم بهترین قالب برای ذخیره پایدار دانش، متن ساده است.
دانش را در متن ساده نگه دارید (نکته ۲۵): با متن ساده، توانایی دستکاری دانش را به صورت دستی و برنامه‌نویسی به خود می‌دهیم.
بیمه در برابر قدیمی شدن: فرم‌های خوانا توسط انسان و داده‌های خودتوصیفی، از تمام فرم‌های دیگر داده و برنامه‌هایی که آن‌ها را ایجاد کرده‌اند عمر طولانی‌تری خواهند داشت.
ارزش افزوده: تقریباً هر ابزاری در جهان محاسبات می‌تواند روی متن ساده کار کند.

---

## ۱۷. بازی‌های شل (Shell Games)

> Every woodworker needs a good, solid, reliable workbench, somewhere to hold work pieces at a convenient height while they're being shaped. For a programmer manipulating files of text, that workbench is the command shell.
> Use the Power of Command Shells (Tip 26): Gain familiarity with the shell, and you'll find your productivity soaring.
> GUI interfaces are wonderful, and they can be faster and more convenient for some simple operations. But if you do all your work using GUIs, you are missing out on the full capabilities of your environment.
> A Shell of Your Own: In the same way that a woodworker will customize their workspace, a developer should customize their shell.

هر نجاری به یک میز کار خوب، محکم و قابل اعتماد نیاز دارد. برای برنامه‌نویسی که با فایل‌های متنی سروکار دارد، آن میز کار، پوسته فرمان (command shell) است.
از قدرت پوسته‌های فرمان استفاده کنید (نکته ۲۶): با پوسته آشنا شوید و بهره‌وری‌تان افزایش خواهد یافت.
رابط‌های GUI فوق‌العاده هستند و برای برخی عملیات ساده می‌توانند سریع‌تر و راحت‌تر باشند. اما اگر تمام کارتان را با GUI انجام می‌دهید، از توانایی‌های کامل محیط خود محروم می‌شوید.
پوسته خودتان: به همان شکلی که یک نجار فضای کار خود را سفارشی می‌کند، یک توسعه‌دهنده باید پوسته خود را سفارشی کند.

---

## ۱۸. ویرایش قدرتمند (Power Editing)

> We've talked before about tools being an extension of your hand. Well, this applies to editors more than to any other software tool.
> Achieve Editor Fluency (Tip 27): By becoming fluent, you no longer have to think about the mechanics of editing. The distance between thinking something and having it appear in an editor buffer drops way down.
> What Does "Fluent" Mean? Moving and making selections by character, word, line, and paragraph. Moving by various syntactic units. Commenting and uncommenting blocks of code with a single command. Undoing and redoing changes. Splitting the editor window into multiple panels.
> Moving Toward Fluency: Learn the commands that make your life easier. Every time you find yourself doing something repetitive, get into the habit of thinking "there must be a better way." Then find it.

قبلاً درباره ابزارهایی کهextension دست شما هستند صحبت کرده‌ایم. خب، این بیش از هر ابزار نرم‌افزاری دیگری در مورد ویرایشگرها صدق می‌کند.
به روانی ویرایشگر برسید (نکته ۲۷): با روان شدن، دیگر لازم نیست درباره مکانیک ویرایش فکر کنید. فاصله بین فکر کردن به چیزی و ظاهر شدنش در بافر ویرایشگر بسیار کم می‌شود.
"روان" یعنی چه؟ حرکت و انتخاب بر اساس کاراکتر، کلمه، خط و پاراگراف. حرکت بر اساس واحدهای نحوی مختلف. نظرگذاری و حذف نظرات با یک دستور واحد. برگرداندن و بازگرداندن تغییرات.
حرکت به سوی روانی: دستوراتی را یاد بگیرید که زندگی‌تان را آسان‌تر می‌کنند.

---

## ۱۹. کنترل نسخه (Version Control)

> Progress, far from consisting in change, depends on retentiveness.
> ➤ George Santayana
>
> Version control systems keep track of every change you make in your source code and documentation. A good VCS will let you track changes, answering questions such as: Who made changes in this line of code? What's the difference between the current version and last week's?
> Always Use Version Control (Tip 28): Always. Even if you are a single-person team on a one-week project. Even if it's a "throw-away" prototype. Make sure that everything is under version control: documentation, phone number lists, memos to vendors, makefiles, build and release procedures.
> Version Control as a Project Hub: Use it to manage your build and deployment processes. Use it to track issues and bugs.

پیشرفت، نه در تغییر، بلکه در حفظ و نگهداری است.
سیستم‌های کنترل نسخه هر تغییری را که در کد منبع و مستندات خود ایجاد می‌کنید ردیابی می‌کنند. یک VCS خوب به شما امکان ردیابی تغییرات را می‌دهد.
همیشه از کنترل نسخه استفاده کنید (نکته ۲۸): همیشه. حتی اگر یک تیم یک نفره در یک پروژه یک هفته‌ای هستید. حتی اگر یک پروتوتایپ "قابل دور ریختن" است. مطمئن شوید همه چیز تحت کنترل نسخه است.
کنترل نسخه به عنوان مرکز پروژه: از آن برای مدیریت فرآیندهای build و deployment استفاده کنید.

---

## ۲۰. اشکال‌زدایی (Debugging)

> It is a painful thing To look at your own trouble and know That you yourself and no one else has made it
> ➤ Sophocles, Ajax
>
> Fix the Problem, Not the Blame (Tip 29): It doesn't really matter whether the bug is your fault or someone else's. It is still your problem.
> Don't Panic (Tip 30): It's easy to get into a panic, especially if you are facing a deadline. But it is very important to step back a pace, and actually think about what could be causing the symptoms.
> Failing Test Before Fixing Code (Tip 31): The best way to start fixing a bug is to make it reproducible.
> Read the Damn Error Message (Tip 32): Read the error message carefully.
> Rubber Ducking: A very simple but particularly useful technique for finding the cause of a problem is simply to explain it to someone else—or to a rubber duck.
> "select" Isn't Broken (Tip 33): Remember, if you see hoof prints, think horses—not zebras.
> Don't Assume It—Prove It (Tip 34): When you come across a surprise bug, beyond merely fixing it, you need to determine why this failure wasn't caught earlier.

دردناک است به مشکل خودت نگاه کنی و بدانی که خودت و نه کس دیگری آن را ایجاد کرده.
مشکل را حل کنید، نه مقصر را (نکته ۲۹): واقعاً مهم نیست اگر باگ تقصیر شماست یا کس دیگر. هنوز مشکل شماست.
وحشت نکنید (نکته ۳۰): آسان است که به وحشت بیفتید، به ویژه اگر با مهلت مواجه هستید. اما بسیار مهم است که یک قدم عقب بنشینید و واقعاً فکر کنید چه چیزی می‌تواند باعث علائم شده باشد.
تست ناموفق قبل از تعمیر کد (نکته ۳۱): بهترین راه برای شروع تعمیر یک باگ این است که آن را قابل بازتولید کنید.
پیام خطا را بخوانید (نکته ۳۲): پیام خطا را دقیق بخوانید.
اردک لاستیکی: تکنیک بسیار ساده اما مفید برای یافتن علت مشکل این است که آن را به کسی توضیح دهید — یا به یک اردک لاستیکی.
"select" خراب نیست (نکته ۳۳): به یاد داشته باشید، اگر رد پای سم دیدید، به اسب فکر کنید — نه زرافه.
فرض نکنید — اثبات کنید (نکته ۳۴): وقتی با یک باگ غافلگیرکننده مواجه شدید، علاوه بر تعمیر آن، باید تعیین کنید چرا این خطا زودتر گرفته نشد.

---

## ۲۱. دستکاری متن (Text Manipulation)

> Pragmatic Programmers manipulate text the same way woodworkers shape wood. Text manipulation languages are to programming what routers are to woodworking.
> Learn a Text Manipulation Language (Tip 35): Using them, you can quickly hack up utilities and prototype ideas—jobs that might take five or ten times as long using conventional languages.

برنامه‌نویسان عملگرا متن را به همان شکلی دستکاری می‌کنند که نجاران چوب را شکل می‌دهند. زبان‌های دستکاری متن در برنامه‌نویسی همان نقشی را دارند که ابزارهای تراش در نجاری.
یک زبان دستکاری متن یاد بگیرید (نکته ۳۵): با استفاده از آن‌ها می‌توانید به سرعت ابزارهای کمکی بسازید و ایده‌ها را پروتوتایپ کنید — کارهایی که با زبان‌های معمولی پنج تا ده برابر طول می‌کشند.

---

## ۲۲. دفترچه‌های روزانه مهندسی (Engineering Daybooks)

> Dave once worked for a small computer manufacturer, which meant working alongside electronic and sometimes mechanical engineers. Many of them walked around with a paper notebook.
> The daybook has three main benefits: It is more reliable than memory. It gives you a place to store ideas that aren't immediately relevant to the task at hand. It acts as a kind of rubber duck.
> So, try keeping an engineering daybook. Use paper, not a file or a wiki: there's something special about the act of writing compared to typing.

دیو زمانی برای یک سازنده کامپیوتر کوچک کار می‌کرد، به این معنی که در کنار مهندسان الکترونیک و گاهی مکانیک کار می‌کرد. بسیاری از آن‌ها با یک دفترچه کاغذی راه می‌رفتند.
دفترچه روزانه سه مزیت اصلی دارد: قابل اعتمادتر از حافظه است. مکانی برای ذخیره ایده‌هایی که فوراً مرتبط با کار فعلی نیستند فراهم می‌کند. به عنوان نوعی اردک لاستیکی عمل می‌کند.
پس، دفترچه مهندسی روزانه داشته باشید. از کاغذ استفاده کنید، نه فایل یا ویکی.

---

# فصل چهارم: شک‌گرایی عملگرا ⏱️ ۲۰ دقیقه مطالعه

## ۲۳. طراحی بر اساس قرارداد (Design by Contract)

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

## ۲۸. جداسازی (Decoupling)

> When we try to pick out anything by itself, we find it hitched to everything else in the Universe.
> ➤ John Muir
>
> Decoupled Code Is Easier to Change (Tip 44): Coupling is the enemy of change, because it links together things that must change in parallel.
> Law of Demeter: Don't talk to strangers. Only talk to your immediate collaborators.
> Avoid Train Wrecks: Chain of method calls is a sign of coupled code.
> Use Intefaces, Not Implementations: Program to an interface, not an implementation.

وقتی سعی می‌کنیم چیزی را به تنهایی انتخاب کنیم، می‌بینیم به همه چیزهای دیگر در جهان متصل است.
کد جداشده تغییر آن آسان‌تر است (نکته ۴۴): جفت‌شدن دشمن تغییر است، چون چیزهایی را که باید همزمان تغییر کنند به هم پیوند می‌دهد.
قانون دمیتر: با غریبه‌ها صحبت نکنید. فقط با همکاران مستقیم خود صحبت کنید.
از قطارهای شکسته اجتناب کنید: زنجیره فراخوانی‌های metod نشانه کد جفت‌شده است.
به interface برنامه‌نویسی کنید، نه پیاده‌سازی.

---

## ۲۹. دنیای واقعی را در دست بگیرید (Juggling the Real World)

> Events are the raw data of the real world. How we model and react to them has a profound effect on the resulting systems.
> Four Strategies for Handling Events:
> - Observer/Publish-Subscribe: Decouple event producers from consumers.
> - Mediator: Centralize event routing.
> - Event Sourcing: Record events, not state.
> - CQRS: Separate reads from writes.

رویدادها داده‌های خام دنیای واقعی هستند. نحوه مدل‌سازی و واکنش به آن‌ها تأثیر عمیقی بر سیستم‌های حاصل دارد.
چهار استراتژی برای مدیریت رویدادها:
- ناظر/انتشار-اشتراک: جفت‌کننده تولیدکنندگان و مصرف‌کنندگان رویداد را جدا کنید.
- واسطه: مسیریابی رویداد را متمرکز کنید.
- انتساب رویداد: رویدادها را ثبت کنید، نه وضعیت را.
- CQRS: خواندن‌ها را از نوشتن‌ها جدا کنید.

---

## ۳۰. تبدیل برنامه‌نویسی (Transforming Programming)

> Code that uses function pipelines tends to be clean, concise, and expressive. It's easy to understand what it does, and it's easy to change.
> pipelines are a natural way to express data transformations.
> Unlike method chains, pipelines pass data through functions without the objects knowing about each other.

کدی که از pipeline های تابعی استفاده می‌کند اغلب تمیز، مختصر و بیانگر است. آسان است بفهمید چه کاری انجام می‌دهد و آسان است تغییرش دهید.

---

## ۳۱. مالیات وراثت (Inheritance Tax)

> Inheritance can be overused. Favor composition over inheritance.
> Delegate, Don't Inherit: When you need to share functionality, consider using composition or delegation instead of inheritance.
> Use the Single Responsibility Principle: A class should have only one reason to change.

وراثت می‌تواند بیش از حد استفاده شود. ترکیب را بر وراثت ترجیح دهید.
واگذار کنید، وراثت ندهید: وقتی نیاز به اشتراک‌گذاری عملکرد دارید، ترکیب یا واگذاری را به جای وراثت در نظر بگیرید.
از اصل مسئولیت واحد استفاده کنید: یک کلاس باید فقط یک دلیل برای تغییر داشته باشد.

---

## ۳۲. پیکربندی (Configuration)

> Configuration is about moving details out of code, where they can be changed more safely and easily.
> Separate Configuration from Code: Configuration should be external to the code.
> Use Convention Over Configuration: When possible, use sensible defaults.
> Keep Configuration Close to the Data: If configuration changes with data, keep them together.

پیکربندی درباره خارج کردن جزئیات از کد است، جایی که می‌توان آن‌ها را با امنیت و آسان‌تر تغییر داد.
پیکربندی را از کد جدا کنید: پیکربندی باید خارج از کد باشد.
از قرارداد بر پیکربندی استفاده کنید: وقتی ممکن است، از پیش‌فرض‌های منطقی استفاده کنید.

---

# فصل ششم: همزمانی ⏱️ ۱۵ دقیقه مطالعه

## ۳۳. شکستن جفت‌شدگی زمانی (Breaking Temporal Coupling)

> Temporal coupling is when two components of a system must execute in a particular order.
> Identify Concurrency Hazards: Look for shared state, race conditions, and deadlocks.
> Be Explicit About Concurrency: Use languages and frameworks that make concurrency explicit.

جفت‌شدگی زمانی زمانی است که دو مولفه سیستم باید به ترتیب خاصی اجرا شوند.
خطرات همزمانی را شناسایی کنید: به دنبال وضعیت مشترک، شرایط مسابقه و بن‌بست باشید.
درباره همزمانی صریح باشید: از زبان‌ها و چارچوب‌هایی استفاده کنید که همزمانی را صریح می‌کنند.

---

## ۳۴. وضعیت مشترک، وضعیت نادرست است (Shared State Is Incorrect State)

> Shared state is a common source of bugs. When multiple threads or processes access the same data, the results can be unpredictable.
> Use Message Passing: Instead of sharing state, share messages.
> Prefer Immutability: Immutable data structures are inherently thread-safe.
> Use Actors or Channels: These provide structured ways to manage concurrent access to state.

وضعیت مشترک منبع رایج باگ‌هاست. وقتی رشته‌ها یا فرآیندهای متعدد به داده‌های یکسان دسترسی دارند، نتایج می‌تواند غیرقابل پیش‌بینی باشد.
از ارسال پیام استفاده کنید: به جای اشتراک‌گذاری وضعیت، پیام‌ها را اشتراک‌گذاری کنید.
تغییرناپذیری را ترجیح دهید: ساختارهای داده تغییرناپذیر ذاتاً thread-safe هستند.

---

## ۳۵. بازیگران و فرآیندها (Actors and Processes)

> Actors are independent units of computation that communicate through message passing.
> Each actor has its own state and processes messages sequentially.
> Actors can create other actors and send messages to other actors.
> This model eliminates many concurrency problems by design.

بازیگران واحدهای مستقل محاسباتی هستند که از طریق ارسال پیام ارتباط برقرار می‌کنند.
هر بازیگر وضعیت خود را دارد و پیام‌ها را به ترتیب پردازش می‌کند.
بازیگران می‌توانند بازیگران دیگری ایجاد کنند و پیام‌هایی به بازیگران دیگر بفرستند.
این مدل بسیاری از مشکلات همزمانی را با طراحی حذف می‌کند.

---

## ۳۶. تابلوهای سیاه (Blackboards)

> Blackboards provide a shared workspace where multiple agents can read and write information.
> They decouple the producers of information from the consumers.
> Different agents can work on the same problem independently, contributing their findings to the blackboard.

تابلوهای سیاه فضای کار مشترکی فراهم می‌کنند که در آن عوامل متعدد می‌توانند اطلاعات را بخوانند و بنویسند.
آن‌ها تولیدکنندگان اطلاعات را از مصرف‌کنندگان جدا می‌کنند.

---

# فصل هفتم: در حین برنامه‌نویسی ⏱️ ۲۰ دقیقه مطالعه

## ۳۷. به مغز خزنده‌ات گوش بده (Listen to Your Lizard Brain)

> Your intuition is valuable. If something feels wrong, it probably is.
> The "lizard brain" is the ancient part of our brain that processes emotions and gut reactions.
> Listen to that nagging feeling that something isn't right—it's trying to tell you something.
> Trust your instincts, but verify with evidence.

اصالت شما ارزشمند است. اگر چیزی اشتباه به نظر می‌رسد، احتمالاً هست.
مغز خزنده بخش باستانی مغز ما است که احساسات و واکنش‌های روده‌ای را پردازش می‌کند.
به آن احساس آزاردهنده که چیزی درست نیست گوش بدهید — دارد سعی می‌کند چیزی به شما بگوید.
به غریزه خود اعتماد کنید، اما با شواهد تأیید کنید.

---

## ۳۸. برنامه‌نویسی بر اساس تصادف (Programming by Coincidence)

> Programmers often confuse "it works" with "it's correct."
> Don't rely on coincidences. Understand why your code works.
> Regression testing helps ensure that changes don't break existing functionality.
> Always ask "why?" when something works.

برنامه‌نویسان اغلب "کار می‌کند" را با "درست است" اشتباه می‌گیرند.
به تصادف‌ها تکیه نکنید. بفهمید چرا کد شما کار می‌کند.
تست‌های بازگشتی کمک می‌کنند تغییرات عملکرد موجود را خراب نکنند.

---

## ۳۹. سرعت الگوریتم (Algorithm Speed)

> Understanding Big-O notation helps you write efficient code.
> O(1): Constant time. The operation takes the same amount of time regardless of input size.
> O(n): Linear time. Time grows proportionally with input size.
> O(n²): Quadratic time. Time grows with the square of input size.
> O(log n): Logarithmic time. Very efficient for large datasets.
> Profile before optimizing. Don't guess—measure.

درک Big-O notation به شما کمک می‌کند کد کارآمد بنویسید.
O(1): زمان ثابت. عملیات بدون توجه به اندازه ورودی زمان یکسانی می‌برد.
O(n): زمان خطی. زمان متناسب با اندازه ورودی رشد می‌کند.
O(n²): زمان درجه دوم. زمان با مجذور اندازه ورودی رشد می‌کند.
O(log n): زمان لگاریتمی. بسیار کارآمد برای مجموعه داده‌های بزرگ.
قبل از بهینه‌سازی پروفایل کنید. حدس نزنید — اندازه بگیرید.

---

## ۴۰. بازآفرینی (Refactoring)

> Refactoring is the process of improving code without changing its behavior.
> Refactor when you need to: when code is duplicated, when logic is complex, when names are unclear.
> Refactoring is not rewriting. It's making small, incremental improvements.
> Keep the code working at all times during refactoring.

بازآفرینی فرآیند بهبود کد بدون تغییر رفتار آن است.
بازآفرینی کنید وقتی نیاز دارید: وقتی کد تکرار شده، وقتی منطق پیچیده است، وقتی نام‌ها نامفهوم هستند.
بازآفرینی بازنویسی نیست. بهبودهای کوچک و تدریجی است.
کد را در تمام مدت بازآفرینی کار نگه دارید.

---

## ۴۱. تست تا کد (Test to Code)

> Testing is not just about finding bugs—it's about designing better software.
> Write tests first (TDD): Write a failing test, make it pass, then refactor.
> Tests serve as documentation: They show how the code is supposed to be used.
> Good tests give you confidence to change code.

تست فقط درباره یافتن باگ نیست — درباره طراحی نرم‌افزار بهتر است.
اول تست بنویسید (TDD): یک تست ناموفق بنویسید، آن را رد کنید، سپس بازآفرینی کنید.
تست‌ها به عنوان مستندات عمل می‌کنند: نشان می‌دهند چگونه باید از کد استفاده شود.

---

## ۴۲. تست مبتنی بر خواص (Property-Based Testing)

> Instead of testing specific examples, test that properties hold for all inputs.
> This finds edge cases that example-based tests might miss.
> Tools like QuickCheck, Hypothesis, or fast-check generate random inputs.

به جای تست مثال‌های خاص، تست کنید که خواص برای تمام ورودی‌ها برقرار باشند.
این موارد حدی را پیدا می‌کند که تست‌های مبتنی بر مثال ممکن است از دست بدهند.

---

## ۴۳. بیرون امن باش (Stay Safe Out There)

> Security is not an afterthought—it must be built in from the start.
> Never trust user input. Always validate and sanitize.
> Use well-tested security libraries. Don't roll your own crypto.
> Keep dependencies updated. Vulnerabilities are discovered daily.

امنیت یک فکر بعدی نیست — باید از ابتدا ساخته شود.
هرگز به ورودی کاربر اعتماد نکنید. همیشه اعتبارسنجی و پاکسازی کنید.
از کتابخانه‌های امنیتی آزمایش شده استفاده کنید.
وابستگی‌ها را به‌روز نگه دارید.

---

## ۴۴. نام‌گذاری چیزها (Naming Things)

> There are only two hard things in Computer Science: cache invalidation and naming things.
> ➤ Phil Karlton
>
> Good names make code readable and maintainable.
> Names should reveal intent. A name should tell you why it exists, what it does, and how it used.
> Avoid encodings. Don't put type information in variable names (like strName or iCount).
> Be consistent. Use the same name for the same concept throughout the codebase.

تنها دو چیز سخت در علوم کامپیوتر وجود دارد: باطل کردن cache و نام‌گذاری چیزها.
نام‌های خوب کد را خوانا و قابل نگهداری می‌کنند.
نام‌ها باید نیت را آشکار کنند. نام باید به شما بگوید چرا وجود دارد، چه کاری انجام می‌دهد و چگونه استفاده می‌شود.
از رمزگذاری اجتناب کنید. اطلاعات نوع را در نام متغیرها قرار ندهید.

---

# فصل هشتم: قبل از پروژه ⏱️ ۱۵ دقیقه مطالعه

## ۴۵. چاه نیازمندی‌ها (The Requirements Pit)

> Requirements are not what the customer says they want. They're what the customer needs.
> The only constant in requirements is change.
> Involve users early and often. Get feedback continuously.
> Don't confuse requirements with implementation details.

نیازمندی‌ها آن چیزی نیست که مشتری می‌گوید می‌خواهد. آن چیزی است که مشتری نیاز دارد.
تنها ثابت در نیازمندی‌ها، تغییر است.
کاربران را زود و مداوم درگیر کنید.
نیازمندی‌ها را با جزئیات پیاده‌سازی اشتباه نگیرید.

---

## ۴۶. حل پازل‌های غیرممکن (Solving Impossible Puzzles)

> When faced with an impossible problem, step back and look at it from a different angle.
> Sometimes the constraints are self-imposed. Challenge assumptions.
> Break the problem down. Look for the simplest solution.
> Ask for help. Two heads are better than one.

وقتی با یک مشکل غیرممکن مواجه هستید، عقب بنشینید و از زاویه دیگری به آن نگاه کنید.
گاهی محدودیت‌ها خودتحمیلی هستند. فرضیات را به چالش بکشید.
مشکل را تقسیم کنید. ساده‌ترین راه‌حل را پیدا کنید.

---

## ۴۷. با هم کار کردن (Working Together)

> Software development is a team sport. No one succeeds alone.
> Communicate constantly. Share knowledge and context.
> Pair programming, mob programming, and code reviews improve code quality.
> Build trust within your team.

توسعه نرم‌افزار یک ورزش تیمی است. هیچ‌کس به تنهایی موفق نمی‌شود.
مداوم ارتباط برقرار کنید. دانش و زمینه را به اشتراک بگذارید.
برنامه‌نویسی جفتی و بررسی کد کیفیت کد را بهبود می‌بخشد.

---

## ۴۸. ماهیت چالاکی (The Essence of Agility)

> Agile is not a methodology. It's a mindset.
> Agile values individuals and interactions over processes and tools.
> Working software over comprehensive documentation.
> Customer collaboration over contract negotiation.
> Responding to change over following a plan.
> Agile doesn't mean no planning. It means planning to adapt.

چالاکی یک روششناسی نیست. یک ذهنیت است.
چالاکی افراد و تعاملات را بر فرآیندها و ابزارها ارزشگذاری می‌کند.
نرم‌افزار کارآمد بر مستندات جامع.
همکاری مشتری بر مذاکره قراردادی.
واکنش به تغییر بر پیروی از طرح.
چالاکی به معنای بدون برنامه‌ریزی نیست. به معنای برنامه‌ریزی برای سازگاری است.

---

# فصل نهم: پروژه‌های عملگرا ⏱️ ۱۵ دقیقه مطالعه

## ۴۹. تیم‌های عملگرا (Pragmatic Teams)

> Pragmatic teams are small, focused, and communicate well.
> Each team member should have a specific area of responsibility, but everyone should be able to step in where needed.
> Build a culture of quality and craftsmanship.
> Automate everything you can.

تیم‌های عملگرا کوچک، متمرکز و خوب ارتباط برقرار می‌کنند.
هر عضو تیم باید مسئولیت خاصی داشته باشد، اما همه باید بتوانند در جای نیاز کمک کنند.
فرهنگ کیفیت و حرفه‌ای بودن بسازید.
هر چیزی که می‌توانید خودکار کنید.

---

## ۵۰. نارگیل‌ها کافی نیستند (Coconuts Don't Cut It)

> Legacy code is code without tests. Legacy systems are systems without documentation.
> Don't let your code become legacy. Write tests. Write documentation.
> Keep your codebase healthy. Refactor regularly.

کد میراث کد بدون تست است. سیستم‌های میراث سیستم‌های بدون مستندات هستند.
بگذارید کد شما میراث نشود. تست بنویسید. مستند بنویسید.
پایگاه کد خود را سالم نگه دارید.

---

## ۵۱. کیت شروع عملگرا (Pragmatic Starter Kit)

> Version control: Always. For everything.
> Regression testing: Automate it. Run it often.
> Version control as a project hub: Use it to manage builds, tests, and deployments.
> Documentation: Write it. Keep it close to the code.

کنترل نسخه: همیشه. برای همه چیز.
تست‌های بازگشتی: خودکار کنید. مداوم اجرا کنید.
کنترل نسخه به عنوان مرکز پروژه: از آن برای مدیریت build، تست و deployment استفاده کنید.
مستندات: بنویسید. آن را نزدیک کد نگه دارید.

---

## ۵۲. کاربرانتان را خوشحال کنید (Delight Your Users)

> The user is not a developer. They don't care about elegant code. They care about results.
> Get feedback early and often. Show working software.
> Manage expectations. Be honest about what you can and can't do.
> Make the simple things easy and the complex things possible.

کاربر یک توسعه‌دهنده نیست. به کد ظریف اهمیتی نمی‌دهد. به نتایج اهمیت می‌دهد.
بازخورد زود و مداوم بگیرید. نرم‌افزار کارآمد نشان دهید.
انتظارات را مدیریت کنید.
ساده را آسان و پیچیده را ممکن کنید.

---

## ۵۳. غرور و تعصب (Pride and Prejudice)

> Take pride in your work. Craftsmanship matters.
> Don't be prejudiced against new technologies or approaches. Give them a fair try.
> Learn from mistakes—yours and others'.
> Share your knowledge. Teach others.

به کارتان افتخار کنید. حرفه‌ای بودن مهم است.
نسبت به فناوری‌ها یا رویکردهای جدید تعصب نداشته باشید.
از اشتباهات بیاموزید — خودتان و دیگران.
دانشتان را به اشتراک بگذارید. به دیگران بیاموزید.

---

## پایان‌نامه (Postface)

> This book is just the beginning. The real learning happens when you apply these ideas.
> Share your experiences. Join the community. Keep learning.
> Remember: it's your life. Make it count.

این کتاب فقط شروع است. یادگیری واقعی زمانی اتفاق می‌افتد که این ایده‌ها را به کار ببرید.
تجربیات خود را به اشتراک بگذارید. به جامعه بپیوندید.
به یاد داشته باشید: زندگی شماست. آن را مهم کنید.