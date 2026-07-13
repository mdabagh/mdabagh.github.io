![System Design Interview: An Insider’s Guide](design-system/images/System-Design-Interview-page1-image1.jpg)



### 1. Original Paragraph

> FORWARD: We are delighted that you have decided to join us in learning the system design interviews. System design interview questions are the most difficult to tackle among all the technical interviews. The questions require the interviewees to design an architecture for a software system, which could be a news feed, Google search, chat system, etc. These questions are intimidating, and there is no certain pattern to follow. The questions are usually very big scoped and vague. The processes are open-ended and unclear without a standard or correct answer. Companies widely adopt system design interviews because the communication and problem solving skills tested in these interviews are similar to those required by a software engineer’s daily work. An interviewee is evaluated based on how she analyzes a vague problem and how she solves the problem step by step. The abilities tested also involve how she explains the idea, discusses with others, and evaluates and optimizes the system. In English, using “she” flows better than “he or she” or jumping between the two. To make reading easier, we use the feminine pronoun throughout this book. No disrespect is intended for male engineers. The system design questions are open-ended. Just like in the real world, there are many differences and variations in the system. The desired outcome is to come up with an architecture to achieve system design goals. The discussions could go in different ways depending on the interviewer. Some interviewers may choose high-level architecture to cover all aspects; whereas some might choose one or more areas to focus on. Typically, system requirements, constraints and bottlenecks should be well understood to shape the direction of both the interviewer and interviewee. The objective of this book is to provide a reliable strategy to approach the system design questions. The right strategy and knowledge are vital to the success of an interview. This book provides solid knowledge in building a scalable system. The more knowledge gained from reading this book, the better you are equipped in solving the system design questions. This book also provides a step by step framework on how to tackle a system design question. It provides many examples to illustrate the systematic approach with detailed steps that you can follow. With constant practice, you will be well-equipped to tackle system design interview questions.

---

## 2. ترجمه تخصصی فارسی

خوشحالیم که تصمیم گرفته‌اید یادگیری مصاحبه‌های طراحی سیستم (System Design Interview) را آغاز کنید.

سؤالات طراحی سیستم از دشوارترین بخش‌های مصاحبه‌های فنی محسوب می‌شوند. در این نوع مصاحبه، از داوطلب انتظار می‌رود معماری (Architecture) یک سیستم نرم‌افزاری مانند News Feed، موتور جستجو، سیستم چت و موارد مشابه را طراحی کند.

این سؤالات معمولاً ترسناک به نظر می‌رسند، زیرا الگوی مشخص و ثابتی برای پاسخ دادن به آن‌ها وجود ندارد. دامنه مسئله بسیار بزرگ است، جزئیات آن مبهم هستند و برخلاف بسیاری از سؤالات برنامه‌نویسی، پاسخ استاندارد یا کاملاً صحیحی برای آن‌ها وجود ندارد.

شرکت‌ها به‌طور گسترده از مصاحبه‌های طراحی سیستم استفاده می‌کنند، زیرا مهارت‌هایی که در این مصاحبه ارزیابی می‌شوند—مانند ارتباط مؤثر، تحلیل مسئله و حل گام‌به‌گام مشکلات—دقیقاً همان مهارت‌هایی هستند که یک مهندس نرم‌افزار در کار روزمره خود به آن‌ها نیاز دارد.

در این مصاحبه، داوطلب بر اساس نحوه تحلیل یک مسئله مبهم، فرآیند رسیدن به راه‌حل، توانایی توضیح ایده‌ها، تعامل و بحث با دیگران، و همچنین ارزیابی و بهینه‌سازی طراحی سیستم مورد سنجش قرار می‌گیرد.

در زبان انگلیسی، استفاده از ضمیر **she** نسبت به عبارت **he or she** روان‌تر است؛ بنابراین در سراسر این کتاب از ضمیر مؤنث استفاده شده است و این موضوع هیچ‌گونه بی‌احترامی نسبت به مهندسان مرد محسوب نمی‌شود.

سؤالات طراحی سیستم ماهیتی باز (Open-ended) دارند. همانند دنیای واقعی، برای یک مسئله می‌توان طراحی‌ها و راهکارهای متفاوتی ارائه داد. هدف اصلی، رسیدن به معماری‌ای است که بتواند اهداف طراحی سیستم را برآورده کند.

روند گفتگو در مصاحبه ممکن است بسته به مصاحبه‌کننده متفاوت باشد. برخی تنها روی معماری سطح بالا (High-Level Architecture) تمرکز می‌کنند، در حالی که برخی دیگر یک یا چند بخش خاص را عمیق‌تر بررسی می‌کنند.

به طور معمول، برای هدایت صحیح مصاحبه، لازم است نیازمندی‌های سیستم (System Requirements)، محدودیت‌ها (Constraints) و گلوگاه‌ها (Bottlenecks) به خوبی شناسایی و درک شوند.

هدف این کتاب ارائه یک استراتژی قابل اعتماد برای مواجهه با سؤالات طراحی سیستم است. داشتن استراتژی مناسب و دانش کافی، نقش بسیار مهمی در موفقیت در این نوع مصاحبه دارد.

این کتاب دانش لازم برای طراحی سیستم‌های مقیاس‌پذیر (Scalable Systems) را ارائه می‌دهد و هرچه دانش بیشتری از آن کسب کنید، آمادگی بیشتری برای پاسخ‌گویی به سؤالات طراحی سیستم خواهید داشت.

همچنین این کتاب یک چارچوب (Framework) گام‌به‌گام برای حل مسائل طراحی سیستم ارائه می‌کند و با مثال‌های متعدد، فرآیند استاندارد پاسخ‌گویی را آموزش می‌دهد. با تمرین مستمر، می‌توانید به سطح مناسبی از آمادگی برای موفقیت در مصاحبه‌های طراحی سیستم برسید.

---

# 3. توضیح از دید یک Software Architect

این مقدمه در واقع می‌خواهد ذهن شما را از **Programming Interview** به **Engineering Interview** منتقل کند.

در مصاحبه‌های الگوریتمی معمولاً سؤال شفاف است:

> دو Sum را حل کن.

در طراحی سیستم سؤال معمولاً این‌گونه است:

> Design Twitter

یا

> Design WhatsApp

اما هیچ توضیح دیگری داده نمی‌شود.

یعنی خودت باید کشف کنی:

* چند کاربر داریم؟
* SLA چیست؟
* Availability مهم‌تر است یا Consistency؟
* آیا میلیون‌ها درخواست داریم؟
* دیتابیس SQL باشد یا NoSQL؟
* آیا Cache لازم است؟
* آیا Microservice مناسب است؟

مصاحبه‌کننده عمداً اطلاعات را کامل نمی‌دهد تا ببیند چگونه مسئله را تحلیل می‌کنی.

در واقع چیزی که ارزیابی می‌شود **جواب نهایی نیست** بلکه **فرآیند فکر کردن (Thinking Process)** است.

این دقیقاً همان کاری است که یک Software Architect هر روز انجام می‌دهد.

---

## 3.1 Knowledge Expansion

### Architecture (معماری)

ساختار کلی سیستم و نحوه ارتباط اجزای مختلف با یکدیگر.

---

### High-Level Architecture

نمای کلی سیستم بدون ورود به جزئیات پیاده‌سازی.

مثلاً فقط مشخص می‌کنیم:

* Client
* API Gateway
* Load Balancer
* Application Servers
* Database
* Cache

نه اینکه کلاس‌ها یا Queryها چگونه نوشته شوند.

---

### Scalability (مقیاس‌پذیری)

توانایی سیستم برای پاسخگویی به افزایش کاربران یا درخواست‌ها بدون افت شدید عملکرد.

---

### Bottleneck (گلوگاه)

بخشی از سیستم که باعث کاهش سرعت کل سیستم می‌شود.

مثلاً:

Database تنها سروری است که تمام درخواست‌ها به آن می‌رسند.

---

### Constraints (محدودیت‌ها)

شرایطی که طراحی باید آن‌ها را رعایت کند.

مثال:

* بودجه محدود
* زمان پاسخ کمتر از 100ms
* Availability بالای 99.99%
* ذخیره اطلاعات به مدت ۱۰ سال

---

## 4. مثال عملی

فرض کنید در مصاحبه گفته می‌شود:

> Design Instagram.

یک پاسخ ضعیف:

> از Laravel استفاده می‌کنم، Redis هم می‌گذارم.

یک پاسخ حرفه‌ای:

1. ابتدا Requirementها را مشخص می‌کنم.
2. تعداد کاربران را می‌پرسم.
3. نوع ترافیک را مشخص می‌کنم.
4. Functional Requirement را استخراج می‌کنم.
5. Non-functional Requirement را مشخص می‌کنم.
6. High-Level Architecture طراحی می‌کنم.
7. Bottleneckها را بررسی می‌کنم.
8. برای Scale راهکار ارائه می‌دهم.

مصاحبه‌کننده دقیقاً این روند را ارزیابی می‌کند.

---

## 5. Visual Learning Mode

```text
                 Client
                 کاربر
                    │
                    ▼
        API Gateway
        درگاه API
                    │
                    ▼
      Load Balancer
      متعادل‌کننده بار
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
 Application Server      Application Server
   سرور برنامه             سرور برنامه
        │                       │
        └───────────┬───────────┘
                    ▼
          Cache (Redis)
          کش (ردیس)
                    │
                    ▼
            Database
          پایگاه داده
```

---

# 7. اصطلاحات مهم

| اصطلاح                  | ترجمه           | تعریف                       | اهمیت                             |
| ----------------------- | --------------- | --------------------------- | --------------------------------- |
| System Design           | طراحی سیستم     | طراحی معماری سیستم‌های بزرگ | موضوع اصلی کتاب                   |
| Architecture            | معماری          | ساختار کلی سیستم            | پایه تمام طراحی‌ها                |
| High-Level Architecture | معماری سطح بالا | نمای کلی سیستم              | اولین مرحله طراحی                 |
| Scalability             | مقیاس‌پذیری     | توانایی رشد سیستم           | مهم‌ترین ویژگی سیستم‌های بزرگ     |
| Constraints             | محدودیت‌ها      | شرایط طراحی                 | تعیین‌کننده راهکار                |
| Bottleneck              | گلوگاه          | عامل محدودکننده عملکرد      | نقطه اصلی بهینه‌سازی              |
| Requirements            | نیازمندی‌ها     | خواسته‌های سیستم            | مبنای طراحی                       |
| Open-ended Question     | سؤال باز        | بدون پاسخ یکتا              | ویژگی اصلی مصاحبه‌های طراحی سیستم |

---

# 8. اشتباهات رایج

* تصور اینکه تنها یک پاسخ صحیح وجود دارد.
* شروع طراحی بدون پرسیدن Requirementها.
* ورود مستقیم به انتخاب فناوری (Technology) به جای تحلیل مسئله.
* تمرکز بیش از حد روی کدنویسی به جای معماری.
* نادیده گرفتن محدودیت‌ها و Bottleneckها.
* توضیح ندادن فرآیند تصمیم‌گیری.

---

# 9. مفاهیم مرتبط

| مفهوم                       | ارتباط                                                 |
| --------------------------- | ------------------------------------------------------ |
| Functional Requirements     | مشخص می‌کند سیستم چه کاری باید انجام دهد.              |
| Non-functional Requirements | کیفیت و ویژگی‌های عملکردی سیستم را تعیین می‌کند.       |
| Scalability                 | هدف اصلی اکثر طراحی‌های سیستم است.                     |
| Load Balancer               | برای توزیع بار بین سرورها استفاده می‌شود.              |
| Database Scaling            | راهکار افزایش ظرفیت پایگاه داده است.                   |
| Caching                     | کاهش فشار روی دیتابیس و افزایش سرعت پاسخگویی.          |
| CAP Theorem                 | در سیستم‌های توزیع‌شده بر تصمیمات معماری اثر می‌گذارد. |

---

# 10. Interview Insight

**چرا این سؤال پرسیده می‌شود؟**

مصاحبه‌کننده می‌خواهد ببیند آیا می‌توانید مانند یک مهندس ارشد فکر کنید، نه صرفاً مانند یک برنامه‌نویس.

**اشتباه رایج**

* شروع مستقیم با تکنولوژی‌ها.
* نپرسیدن سؤال برای شفاف‌سازی مسئله.
* نداشتن ساختار در ارائه راه‌حل.

**پاسخ خوب**

ابتدا نیازمندی‌ها را مشخص کنید، سپس معماری سطح بالا را طراحی کنید، بعد اجزا را به‌تدریج با در نظر گرفتن محدودیت‌ها، گلوگاه‌ها و مقیاس‌پذیری تکمیل کنید.

---

# 11. Interview Deep Dive

* **Difficulty:** Easy (مقدماتی)
* **FAANG Frequency:** ★★★★★

**سؤالات ادامه‌دار رایج**

* Functional و Non-functional Requirement چیست؟
* چگونه Bottleneckها را پیدا می‌کنید؟
* چرا Redis اضافه می‌کنید؟
* چه زمانی Database را Sharding می‌کنید؟
* اگر کاربران ۱۰۰ برابر شوند چه تغییری در معماری می‌دهید؟

---

# 12. ارتباط با دنیای واقعی

این مقدمه پایه تمام موضوعات پیشرفته‌ای است که در ادامه کتاب با آن‌ها مواجه خواهید شد، از جمله:

* **DDD** برای مدل‌سازی دامنه کسب‌وکار.
* **CQRS** برای جداسازی خواندن و نوشتن.
* **Microservices** برای تقسیم سیستم‌های بزرگ.
* **Redis** برای کش و افزایش Performance.
* **Kafka/RabbitMQ** برای پردازش ناهمزمان.
* **Docker** و **Kubernetes** برای استقرار و مقیاس‌پذیری.
* **Database Scaling** برای مدیریت حجم بالای داده و ترافیک.

---

# 13. Memory Hook

**در System Design، مسیر رسیدن به پاسخ مهم‌تر از خود پاسخ است.**

---

# 14. Flashcards

**Q1:** چرا سؤالات System Design پاسخ قطعی ندارند؟
**A:** چون محدودیت‌ها، نیازمندی‌ها و Trade-offها در هر سناریو متفاوت هستند.

---

**Q2:** مهم‌ترین معیار ارزیابی در مصاحبه طراحی سیستم چیست؟
**A:** فرآیند تحلیل مسئله، تصمیم‌گیری و استدلال معماری.

---

**Q3:** اولین قدم در پاسخ به یک سؤال System Design چیست؟
**A:** شفاف‌سازی نیازمندی‌ها، محدودیت‌ها و فرضیات.

---

**Q4:** منظور از High-Level Architecture چیست؟
**A:** نمایش اجزای اصلی سیستم و نحوه ارتباط آن‌ها بدون ورود به جزئیات پیاده‌سازی.

---

**Q5:** چرا شرکت‌ها از مصاحبه‌های طراحی سیستم استفاده می‌کنند؟
**A:** زیرا مهارت‌های تحلیل، ارتباط، طراحی و حل مسئله در این مصاحبه مشابه چالش‌های واقعی مهندسان نرم‌افزار است.